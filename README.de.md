# Lane4 PHP Docker Images

### Provision of PHP-Based Docker Images for Web Stacks and Console Applications

Our goal is to provide various PHP-based Docker images, ranging from development and testing to production environments.

This repository consists of **3 professional PHP-based Docker images** tailored for the following application contexts:

- **Console**: `phpCLI`
- **WebStacks**:
  - **Classic**: `nginx`, `php-fpm`, `mariadb`, `redis`
  - **Application Server**: `roadrunner`, `mariadb`, `redis`

## Prerequisites

Before you can use the Docker images, please ensure that the following prerequisites are met:

1. **Docker** and **Docker Compose** must be installed and correctly configured on your system. You can verify the installation by running the following commands in your terminal:
    ```bash
    docker --version
    docker-compose --version
    ```

## Installation and Usage

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/lane4hub/docker.git
    cd docker
    ```

2. **Working Directories**: For the desired Docker images, navigate to the corresponding working directory (e.g., `phpCli`). There, you will find additional `README.md` files with the necessary instructions.

---

## Contact and Support

For questions or issues, please open an [Issue](https://github.com/lane4hub/docker/issues) in this repository.
