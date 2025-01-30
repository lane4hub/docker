# Lane4 Digital PHP CLI

![Build Status](https://github.com/lane4hub/docker/actions/workflows/phpCli.yml/badge.svg)
[![Docker Image Version](https://img.shields.io/docker/v/lane4hub/phpcli?sort=semver)](https://hub.docker.com/r/lane4hub/phpcli)

### Providing Versioned PHP Docker Images for Console Applications

The **Lane4 Digital PHP CLI** tool is designed to deliver cross-platform PHP-CLI Docker images. It supports PHP versions from **7.4 to 8.3**, enabling developers and administrators to create and maintain consistent and reliable environments for their console applications.

Our Docker images are available for both **AMD64** and **ARM64** architectures and are hosted on [Docker Hub](https://hub.docker.com/r/lane4hub/phpcli). This ensures broad compatibility and allows deployment across various hardware platforms, including modern servers and IoT devices.

1. **PHP Version**: Supports various PHP versions using the `PHP_VERSION` build argument.
- `versions` (7.4, 8.0, 8.1, 8.2 8.3)
2. **Extensions**: Includes commonly used PHP extensions:
- `pdo`, `pdo_mysql`, `mysqli` (database support)
- `redis` (Caching),
- `curl` (HTTP requests)
- `soap` (SOAP services)
- `dom` `zip` (file and XML processing),
- `mbstring` (multibyte string processing)
- `pcntl` (multi process)

3. **Xdebug**:
- Automatically installs the appropriate Xdebug version:
  - Xdebug 3.1.6 for PHP 7.4.
  - Latest Xdebug version for PHP >= 8.0.
- Enabled for debugging and profiling.

4. **Composer**:
- Latest `composer` command is pre-installed and ready to use.

5. **Minimal Overhead**:
- Based on `alpine`, a very lightweight Linux distribution, to keep the image size small.

6. **User-Friendly Configuration**:
- Pre-configured with `php.ini` in production mode, but easily customizable.

7. **Two-Stage Build**:
- The build process is divided into two stages:
  - **Build Phase**: Installs and configures dependencies and PHP extensions.
  - **Runtime Phase**: Only essential files are transferred to the runtime environment, reducing the image size.

## Prerequisites

Please refer to the installation prerequisites outlined in the `README.md` located in the root directory of the Docker project repository.

## Usage

We have created a `Makefile` that provides all available usage options through the `make` command in the terminal.

## Customization for Your Needs

If you wish to fully customize the tool to meet your specific requirements, please edit the relevant entries in the `.env` file.

This allows for flexible configuration of the provided Docker images, including specific PHP extensions, configuration settings, and other customizations.

For this type of usage, you will need your own source and image repository.

We would greatly appreciate it if you could acknowledge us as a supporter of your Docker images in such cases.

## Contents of `phpCli`

The `phpCli` package includes the following components:

- **Source Files**:
    - `/phpcli` – Contains the source code and configuration files for the PHP-CLI tool.

- **Support Files**:
    - `.env` – Environment variables for configuring the Docker images.
    - `docker-compose.yml` – Docker Compose configuration file for orchestrating the containers.
    - `Dockerfile` – Dockerfile for building the PHP-CLI images.
    - `Makefile` – Simple command-line helper. Run `make` in the terminal to view available commands.
    - `.github/workflows/phpCli.yml` – GitHub Actions workflow for automating builds and tests.

- **Documentation**:
    - `README.md` – Comprehensive documentation and guides for using the tool.

## Examples of Usage

```bash
docker build --build-arg PHP_VERSION=8.1 -t my-php-image .
docker run --rm -v $(pwd):/app -w /app my-php-image php script.php
```
