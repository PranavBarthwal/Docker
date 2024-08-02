# 🐳DOCKER

## Environment Consistency Problem
Different environments (development, testing, production) may have different configurations, dependencies, and versions, leading to the classic "it works on my machine" problem.
Docker ensures that the application runs in a consistent environment across all stages. By packaging the application and its dependencies into a container, Docker guarantees that it will behave the same way regardless of where it is deployed.


## What is Docker?

Docker is an open-source platform designed to automate the deployment, scaling, and management of applications. It allows developers to package applications and their dependencies into a standardized unit called a container. This ensures that the application runs consistently across different environments, from development to production.

### Key Concepts

1. **Containers**:
    - Containers are lightweight, portable, and self-sufficient units that include everything needed to run a piece of software, such as code, runtime, libraries, and system tools.
    - They share the host system's kernel but operate in isolation, providing a consistent runtime environment.

2. **Images**:
    - Docker images are read-only templates used to create containers. They include the application code, libraries, and dependencies required to run the application.
    - Images can be built from a set of instructions written in a `Dockerfile`.

3. **Dockerfile**:
    - A `Dockerfile` is a text document containing a series of instructions on how to build a Docker image.
    - Each instruction in a `Dockerfile` creates a layer in the image, contributing to the final build.

4. **Docker Engine**:
    - Docker Engine is the underlying client-server technology that builds and runs containers.
    - It consists of a server (`dockerd`), a REST API, and a client (`docker`).

5. **Docker Hub**:
    - Docker Hub is a cloud-based registry service where Docker users and partners can create, test, store, and distribute container images.
    - It provides a central repository to find and share container images.

## Docker Architecture

<div style="display: flex" align="center">

 ![alt text](./img/image-1.png) Single Container 

![alt text](<./img/Screenshot 2024-08-02 124230.png>) Multiple containers for multiple apps

</div>


## Running multiple versions of same application

<div style="display: flex" align="center">

![alt text](<./img/Screenshot 2024-08-02 124933.png>)

</div>



## Docker vs Virtual Machines (VMs)

| Feature             | Docker Containers                 | Virtual Machines (VMs)         |
|---------------------|-----------------------------------|--------------------------------|
| **Architecture**    | Shares host OS kernel             | Full OS including guest OS     |
| **Performance**     | Near-native performance           | Higher overhead                |
| **Resource Usage**  | Lightweight, efficient            | Resource-intensive             |
| **Startup Time**    | Fast (seconds)                    | Slower (minutes)               |
| **Portability**     | Highly portable                   | Less portable                  |
| **Isolation**       | Process-level isolation           | Hardware-level isolation       |
| **Use Cases**       | Microservices, CI/CD, Dev/Test    | Full OS, legacy apps, isolation|

---
