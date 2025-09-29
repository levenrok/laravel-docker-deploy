# Dockerized Laravel Environment

A production-ready Docker template for deploying Laravel applications using PHP 8.4, PHP-FPM, and Nginx. This setup is designed with security in mind, running the server as a non-root user.

## Features

-   **PHP 8.4**
-   **Nginx**
-   **PHP-FPM** & **Supervisor**
-   Runs as a **non-root user** for enhanced security.
-   Optimized for production deployment.

## Prerequisites

-   Docker installed on your machine.
-   A Docker Hub account (or another container registry).

## Getting Started

You can integrate this Docker setup into a new or existing Laravel project.

### For a New Laravel Project

1.  **Clone this repository:**
    ```bash
    git clone https://github.com/levenrok/laravel-docker-deploy.git my-laravel-app
    cd my-laravel-app
    ```

2.  **Create your Laravel project inside the directory.** If you have Composer installed locally, you can run:
    ```bash
    composer create-project --prefer-dist laravel/laravel .
    ```

3.  **(Optional) Initialize a new Git repository:**
    ```bash
    rm -rf .git
    git init && git add . && git commit -m "Initial commit"
    ```

### For an Existing Laravel Project

If your project directory is not empty, you can't clone directly into it. Instead, copy the deployment files.

1.  **Clone this template into a temporary folder:**
    ```bash
    git clone https://github.com/levenrok/laravel-docker-deploy.git laravel-docker-template
    ```

2.  **Copy the template files into your project's root directory:**
    ```bash
    # Make sure you are in your project's root directory
    cp -R laravel-docker-template/docker .
    cp laravel-docker-template/.dockerignore .
    cp laravel-docker-template/docker-compose.yml .
    cp laravel-docker-template/Dockerfile .
    ```

3.  **Clean up the temporary folder:**
    ```bash
    rm -rf laravel-docker-template
    ```

## Configuration

Before building, customize the `docker-compose.yml` file to match your project and registry details.

```yaml
services:
  app:
    # Change the container name to something unique for your project
    container_name: my-laravel-app
    # Update the image name to your Docker Hub repository and project name
    image: your-dockerhub-username/my-laravel-app:latest
    build: .
# ...
```

## Usage

1.  **Build the Docker Image:**
    This command builds the image using the `Dockerfile` in the current directory.
    ```bash
    docker compose build --no-cache
    ```

2.  **Test the Container Locally:**
    Run the container to ensure there are no build or runtime errors.
    ```bash
    docker compose up --force-recreate
    ```
    You can verify that the container is running with `docker ps`.

3.  **Push to Docker Hub:**
    Once you've confirmed the image works, push it to your container registry.
    ```bash
    docker compose push
    ```
    Your application is now ready to be deployed on any server with Docker.

## Acknowledgements

This template was inspired by the work and tutorials from the [Emad Zaamout](https://youtube.com/@emadzaamout?si=ymPxQtFGY-FSoXaI) YouTube channel.