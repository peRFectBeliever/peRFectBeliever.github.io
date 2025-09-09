
+++
authors = ["Devendran Nehru"]
title = "Docker Notes"
date = "2025-07-30"
description = "Notes for Docker"
tags = [
    "devops",
    "docker",
    "tools",
]
categories = [
    "Database",
    "StudyNotes",
]
series = ["StudyNotes"]
+++


# Docker: From Novice to Pro 🐳

Docker is an open-source platform that simplifies the process of creating, deploying, and running applications by using containers. A **container** is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings.

---

## Brief History

Before Docker, developers often faced the "it works on my machine" problem, where an application would run perfectly in their local development environment but fail when deployed to a production server due to differences in dependencies, libraries, or operating systems. Virtual machines (VMs) were a solution, but they were resource-intensive. VMs virtualize an entire hardware stack and run a full-fledged operating system for each application.

Docker was first introduced in 2013 by Solomon Hykes at Docker Inc. It leveraged existing Linux technologies like cgroups and namespaces to create a more efficient alternative to VMs. Instead of virtualizing the entire hardware stack, Docker containers share the host operating system's kernel, making them much faster and more lightweight. This led to rapid adoption and revolutionized the way software is packaged and deployed.

---

## Logical Components of Docker

Docker's core functionality is built around three main logical components: **images**, **containers**, and **registries**.

* **Docker Images:** An image is a read-only template that contains the application and all its dependencies. Think of it as a blueprint or a class in object-oriented programming. You can build an image from a **Dockerfile**, which is a text file that contains a set of instructions for building the image.
* **Docker Containers:** A container is a runnable instance of an image. It's the actual, living application. You can start, stop, move, or delete a container. Multiple containers can be run from the same image, each completely isolated from the others.
* **Docker Registries:** A registry is a centralized repository for storing and distributing Docker images. The most well-known public registry is **Docker Hub**. You can push your custom-built images to a registry and pull images created by others. This allows for easy sharing and collaboration.

---

## Docker Workflow

The typical Docker workflow is a straightforward process.

1.  **Write a Dockerfile:** A developer creates a `Dockerfile` that specifies the base image and the steps to build their application image (e.g., copying application files, installing dependencies, and exposing ports).
2.  **Build the Image:** The `docker build` command uses the `Dockerfile` to create a Docker image. This image is stored locally in the developer's machine.
3.  **Push to a Registry:** Once built, the image can be pushed to a Docker registry (like Docker Hub) using `docker push`, making it accessible to others.
4.  **Pull and Run the Container:** Other developers or production servers can pull the image from the registry using `docker pull`. They can then run a container from that image using `docker run`, which starts the application. The container is isolated from the host and other containers, ensuring a consistent runtime environment.

---

## Docker Software Components & WSL Setup

The core Docker software is made up of a few key components:

* **Docker Engine:** This is the heart of Docker. It includes the **Docker Daemon** (a background process that manages images, containers, volumes, etc.), the **Docker CLI** (the command-line tool that lets you interact with the daemon), and a REST API.
* **Docker Compose:** A tool for defining and running multi-container Docker applications. It uses a single YAML file to configure all the application's services.
* **Docker Desktop:** An easy-to-install application for Mac, Windows, and Linux that provides a user-friendly interface and packages the Docker Engine, Docker CLI, and other tools.

### Setting up Docker in WSL 2 on Windows

1.  **Install WSL 2:** Ensure you have WSL 2 enabled on your Windows machine. Open PowerShell as an administrator and run:
    ```
    wsl --install
    ```
2.  **Download Docker Desktop:** Go to the official Docker website and download Docker Desktop for Windows.
3.  **Install Docker Desktop:** Run the installer and follow the on-screen instructions.
4.  **Enable WSL 2 Integration:** Once installed, open Docker Desktop, go to **Settings**, navigate to the **Resources > WSL Integration** section, and enable integration for your desired WSL 2 distribution (e.g., Ubuntu).
5.  **Verify Installation:** Open your WSL terminal (e.g., Ubuntu) and run:
    ```
    docker run hello-world
    ```
    This command pulls and runs a small test image, confirming that Docker is correctly configured and working within your WSL environment.

---

## Frequently Faced Issues

* **Permission Errors:** `Got permission denied while trying to connect to the Docker daemon socket` can be solved by adding your user to the `docker` group with `sudo usermod -aG docker $USER`.
* **Container Port Conflicts:** If you try to map a container port to a host port that is already in use, Docker will fail. Use `docker ps` to find existing container ports or choose a different port for your new container.
* **Image Not Found:** This often means you've misspelled the image name or tag. Double-check the name and run `docker images` to see your local images.
* **WSL 2 not starting:** This can happen if the WSL 2 kernel is not updated. Run `wsl --update` to fix it.

---

## Example Sections with Frequently Used Commands

### Basic Docker Commands

| Command | Description | Example |
| :--- | :--- | :--- |
| **`docker build`** | Builds a Docker image from a Dockerfile. | `docker build -t my-app .` |
| **`docker run`** | Creates and starts a container from an image. | `docker run -p 8080:80 my-app` |
| **`docker ps`** | Lists running containers. Add `-a` to show all containers. | `docker ps -a` |
| **`docker stop`** | Stops a running container. | `docker stop <container_id_or_name>` |
| **`docker rm`** | Removes a stopped container. | `docker rm <container_id_or_name>` |
| **`docker rmi`** | Removes an image. | `docker rmi my-app:latest` |
| **`docker pull`** | Pulls an image from a registry. | `docker pull nginx:latest` |
| **`docker push`** | Pushes an image to a registry. | `docker push myuser/my-app:1.0` |

---

### Docker Compose Commands

Docker Compose simplifies multi-container applications.

* `docker-compose up`: Builds, creates, and starts all services defined in the `docker-compose.yml` file. Add `-d` to run in detached mode.
* `docker-compose down`: Stops and removes containers, networks, and volumes created by `docker-compose up`.

**Example `docker-compose.yml` file:**
```
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  db:
    image: postgres:latest
    environment:
    POSTGRES_PASSWORD: mysecretpassword
```

## References
[https://riptutorial.com/Download/docker.pdf](https://riptutorial.com/Download/docker.pdf)
[https://github.com/veggiemonk/awesome-docker](https://github.com/veggiemonk/awesome-docker)
