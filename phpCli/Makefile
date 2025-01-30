SHELL := bash
.SHELLFLAGS := -eu -o pipefail -c
MAKEFLAGS += --warn-undefined-variables
DOCKER_COMPOSE := docker compose

include .env
export PUID ?= $(shell id -u)
export PGID ?= $(shell id -g)

NO_CACHE ?= true

# Selection of PHP versions to build docker images
PHP_VERSIONS := 7.4 8.0 8.1 8.2 8.3 8.4
LATEST_VERSION := $(word $(words $(PHP_VERSIONS)),$(PHP_VERSIONS))

help:
	@echo -e "\033[0;32m Usage: make [target] "
	@echo
	@echo -e "\033[1m targets:\033[0m"
	@egrep '^(.+):*\ ##\ (.+)' ${MAKEFILE_LIST} | column -t -c 2 -s ':#'
.PHONY: help

<---docker------->: ## -----------------------------------------------------------------------
build: ## Build local native platform php image for .env PHP_VERSION
	$(DOCKER_COMPOSE) build \
	$$( [ "$(NO_CACHE)" = "true" ] && echo "--no-cache" ) \
	$(PHP_IMAGE_NAME)
	docker images --filter dangling=true -q | xargs -r docker rmi
.PHONY: build

build-all-versions-local: ## Build local native platform php image for all defined PHP_VERSIONS
	@for version in $(PHP_VERSIONS); do \
		echo ">>> Building php-cli for PHP $$version ..."; \
		PHP_VERSION=$$version $(DOCKER_COMPOSE) build \
		$$( [ "$(NO_CACHE)" = "true" ] && echo "--no-cache" ) \
		$(PHP_IMAGE_NAME); \
		echo ">>> Created: php-cli (PHP $$version)"; \
	done
	docker images --filter dangling=true -q | xargs -r docker rmi
.PHONY: build-all-versions-local

build-multiplatform-for-remote: buildx-create ## Build und push multiplatform (arm64 + amd64) for all defined versions
	@for version in $(PHP_VERSIONS); do \
		echo ">>> Building php-cli:$$version (multiarch) ..."; \
		docker buildx build \
		  --platform linux/amd64,linux/arm64 \
		  --provenance=mode=max \
		  --attest=type=sbom \
		  --build-arg PHP_VERSION=$$version \
		  $$( [ "$(NO_CACHE)" = "true" ] && echo "--no-cache" ) \
		  -t $(DOCKER_HUB)/$(PHP_IMAGE_NAME):$$version \
		  --push \
		  -f dockerfile \
		  .; \
		echo ">>> Created: php-cli:$$version (multiarch)"; \
	done; \
	# Falls die letzte Version ist, wird das 'latest' Tag erstellt
	echo ">>> Setting latest tag for php-cli:$(LATEST_VERSION) ..."; \
	docker buildx imagetools create \
		-t $(DOCKER_HUB)/$(PHP_IMAGE_NAME):latest \
		$(DOCKER_HUB)/$(PHP_IMAGE_NAME):$(LATEST_VERSION); \
	echo ">>> Pushed latest tag for php-cli:$(LATEST_VERSION)"; \
	docker images --filter dangling=true -q | xargs -r docker rmi
.PHONY: build-multiplatform-for-remote

build-multiplatform-remote-latest: buildx-create ## Build und push multiplatform (arm64 + amd64) for latest version
	docker buildx build \
	  --platform linux/amd64,linux/arm64 \
	  --provenance=mode=max \
	  --attest=type=sbom \
	  --build-arg PHP_VERSION=$(LATEST_VERSION) \
	  $$( [ "$(NO_CACHE)" = "true" ] && echo "--no-cache" ) \
	  -t $(DOCKER_HUB)/$(PHP_IMAGE_NAME):latest \
	  --push \
	  -f dockerfile \
	  .
.PHONY: build-multiplatform-remote-latest

buildx-create: ## Creates multiarch-builder
	@docker buildx ls | grep multiarch-builder || docker buildx create --name multiarch-builder --use
.PHONY: buildx-create

remove: ## Stops and removes containers, images and caches
	$(DOCKER_COMPOSE) down --volumes --remove-orphans --rmi "all"
	docker images --filter dangling=true -q | xargs -r docker rmi
.PHONY: remove

shell: ## Run a shell inside the container
	$(DOCKER_COMPOSE) run --rm -it $(PHP_IMAGE_NAME) sh
.PHONY: shell

<---ssh agent---->: ## -----------------------------------------------------------------------
ssh-agent: ## Get SSH agent ready
	eval `ssh-agent -s`
	ssh-add
.PHONY: ssh-agent
