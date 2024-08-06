# 🐳DOCKER

## 0. Environment Consistency Problem
Different environments (development, testing, production) may have different configurations, dependencies, and versions, leading to the classic "it works on my machine" problem.
Docker ensures that the application runs in a consistent environment across all stages. By packaging the application and its dependencies into a container, Docker guarantees that it will behave the same way regardless of where it is deployed.

<br>

## 1. What is Docker?

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

<br>

## 2. Docker Architecture

<div style="display: flex" align="center">

 ![alt text](./img/image-1.png) <br>Single Container </br>

![alt text](<./img/Screenshot 2024-08-02 124230.png>) <br>Multiple containers for multiple apps</br>

</div>
<br>

## 3. Running multiple versions of same application

<div style="display: flex" align="center">

![alt text](<./img/Screenshot 2024-08-02 124933.png>)

</div>
<br>

## 4. Docker vs Virtual Machines (VMs)

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

<br>

## 5. Main Components of Docker

- **Docker File** : A Dockerfile is a script containing a series of instructions on how to build a Docker image. Each instruction in the Dockerfile adds a layer to the image, and when executed, it constructs a complete image that can be used to create containers. These containers are instances of the image, running isolated and portable environments for your applications.
- **Docker Image** : A Docker image is a lightweight, standalone, and executable software package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and configuration files. Docker images are used to create containers, which are instances of these images running as isolated processes on a host operating system.
- **Docker Container** : A Docker container is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, libraries, and settings. Containers are created from Docker images and can run on any system that has the Docker platform installed, ensuring consistency across different environments.
- **Docker Registry** : A Docker registry is a centralized repository where Docker images are stored, managed, and distributed. It allows users to share and deploy images easily across different environments. Registries can be public or private, with **Docker Hub** being the most well-known public registry.

<br>

## 6. Flow of Docker 

![alt text](<./img/Screenshot 2024-08-05 143529.png>)
![alt text](<./img/Screenshot 2024-08-05 144148.png>)

<br>

## 7. Creating Dockerfile, Image and Container

This Dockerfile is used to create a Docker image with Node.js installed, suitable for running a Node.js application.

###  🐳 Dockerfile Content

```Dockerfile
# Base image: Here we are using the official Node.js image. 
# We can specify a specific version of the Node.js image, in this case, version 20.
FROM node:20

# Working directory: Setting the working directory to /myapp (this will create the directory in the container if it doesn't exist).
WORKDIR /myapp

# Copying all files from the current directory on the host to the /myapp directory in the container.
COPY . .

# Installing all dependencies specified in package.json.
RUN npm install

# Exposing the port 3000. This informs Docker that the container listens on this network port at runtime.
EXPOSE 3000

# Running the application using npm start, which should be defined in the package.json file's scripts section.
CMD ["npm", "start"]
```

### 🐳 Building the Docker Image

To build the Docker image using the Dockerfile, run the following command in the terminal:

```sh
docker build -t your-image-name .
```

or 

```sh
docker build .
```

* `-t your-image-name` tags the image with a name. Replace `your-image-name` with a suitable name for your image.
* `.` refers to the current directory, where the Dockerfile is located.

### 🐳 Verifying the Docker Image

After building the image, you can verify its creation by running:

```sh
docker images ls
```

This command lists all Docker images available on your system.

### 🐳 Running the Docker Image

To run the Docker image, you have two options:
1. **Without port binding**: Run the container without exposing it to a specific port on the host machine.

    ```sh
    docker run your-image-name
    ```

2. **With port binding**: Bind the port 3000 of the container to the port 3000 of the host machine. This allows you to access the application on your host machine's port 3000.

    ```sh
    docker run -p 3000:3000 your-image-name
    ```

3. **With port binding in Detached Mode :** Running a Docker container in detached mode allows the container to run in the background, independent of the terminal session. This is useful for long-running applications or services, as it frees up the terminal for other tasks. To run a Docker container in detached mode, use the `-d` flag with the `docker run` command:

    ```sh
    docker run -d -p 3000:3000 your-image-name
    ```


### 🐳 Checking Running Containers

To check if the Docker container is running, use the following command:

```sh
docker ps
```

This command lists all running Docker containers.

### 🐳 Checking All containers (Running or not)

To check all Docker containers, whether they are running or stopped, you can use the following command:

```sh
docker ps -a
```

This command lists all containers on your system, providing details such as container IDs, image names, commands used to start them, creation time, status, ports, and names.

### 🐳 Stopping the Docker Container

To stop the running Docker container, use the following command:

```sh
docker stop <container-id>
```

Replace `<container-id>` with the ID or name of the container you wish to stop. You can find the container ID or name from the `docker ps` output.

### 🐳 Removing Container
To remove a Docker container, you need to know its container ID or name. Follow these steps:

1. **List all containers** (both running and stopped) to find the container ID or name:

    ```sh
    docker ps -a
    ```

2. **Remove the container** using the `docker rm` command followed by the container ID or name. For example, to remove a container with the ID `abc123`:

    ```sh
    docker rm abc123
    ```

### 🐳 Removing Running Containers

If the container is currently running, you need to stop it before removing it. You can do this in one command by adding the `-f` (force) flag, which stops and removes the container:

```sh
docker rm -f abc123
```

### 🐳 Removing All Containers

To remove all containers, you can use the following command, which stops and removes all containers:

```sh
docker rm -f $(docker ps -aq)
```

* `docker ps -aq` lists all container IDs.
* `docker rm -f` removes all containers, even if they are running.

Use these commands with caution, especially the one that removes all containers, as this action cannot be undone.

### 🐳 Auto Removing when Container is stopped
To automatically remove a Docker container when it stops, you can use the `--rm` flag with the `docker run` command. This will ensure that the container is removed immediately after it stops, without needing any manual intervention.

```sh
docker run --rm -d -p 3000:3000 your-image-name
```
### 🐳 Custom name to container
```sh
docker run -d --rm --name "dockertutorial" -p 3007:3000 5feb38d50bc3
```

<br>

## 8. Running Multiple Containers of the Same Image

You can run multiple instances of the same Docker image, each listening on a different port on the host machine. This allows you to scale your application or test different configurations simultaneously. Here’s how to do it:

### 🐳 Commands to Run Multiple Containers

```sh
docker run -d -p 3000:3000 5feb38d50bc3
docker run -d -p 3001:3000 5feb38d50bc3
docker run -d -p 3002:3000 5feb38d50bc3
```

### 🐳 Explanation

1. **First Container**: 
    ```sh
    docker run -d -p 3000:3000 5feb38d50bc3
    ```
    This command runs the container in detached mode (`-d`) and maps port 3000 on the host to port 3000 in the container. The container is created from the image with ID `5feb38d50bc3`.

2. **Second Container**:
    ```sh
    docker run -d -p 3001:3000 5feb38d50bc3
    ```
    This command also runs the container in detached mode but maps port 3001 on the host to port 3000 in the container. Even though the container is using port 3000 internally, it’s accessible on port 3001 on the host machine.

3. **Third Container**:
    ```sh
    docker run -d -p 3002:3000 5feb38d50bc3
    ```
    Similar to the previous commands, this one runs the container in detached mode and maps port 3002 on the host to port 3000 in the container.

### 🐳 Benefits

1. **Testing and Development**: Running multiple containers from the same image on different ports allows you to test different scenarios or configurations without interference.
2. **Load Balancing and Scaling**: This setup is useful for load balancing and scaling applications. You can distribute traffic across multiple containers to handle higher loads.
3. **Isolation**: Each container runs in isolation, so changes in one container won’t affect the others. This is useful for ensuring consistent behavior across different environments.

### 🐳 Verifying Running Containers

To verify that all containers are running, use the following command:

```sh
docker ps
```

This will list all running Docker containers, including their port mappings.

### 🐳 Stopping the Containers

To stop the running containers, use the `docker stop` command followed by the container IDs or names. For example:

```sh
docker stop <container-id-1> <container-id-2> <container-id-3>
```

Replace `<container-id-1>`, `<container-id-2>`, and `<container-id-3>` with the actual container IDs from the `docker ps` output.

<br>

## 9. Managing Docker Images

### 🐳 Assigning Tag/Name to Docker Image

- `docker build`: This is the base command to build a Docker image.
- `-t mydockercont:01`: This tags the image with the name `mydockercont` and the tag `01`. The tag is optional but useful for versioning.
- `.`: This indicates the build context, which is the current directory in this case.
    ```Sh
    docker build -t mydockercont:01 .
    ```

### 🐳 Removing Docker Image

-  `rmi` : *rm* stand for remove and additional *i* for Removing images
    ```Sh
    docker rmi mydockercont:01
    ```

<br>

## 10. Pre defined Images on DockerHub

Docker Hub is a repository of predefined Docker images that you can use to quickly set up various applications and services. One popular example is the Nginx web server.

### Using Predefined Nginx Image

1. **Pulling the Nginx Image**:

    To pull the official Nginx image from Docker Hub, use the following command:

    ```sh
    docker pull nginx
    ```

    This downloads the latest Nginx image to your local machine. You can also specify a version or tag if needed, e.g., `nginx:1.21.3`.

2. **Running the Nginx Container**:

    To run the Nginx container in detached mode and map port 80 on the host to port 80 in the container, use the following command:

    ```sh
    docker run -d --name mynginx -p 8080:80 nginx
    ```

    - `-d`: Runs the container in detached mode (in the background).
    - `--name mynginx`: Assigns the name `mynginx` to the container.
    - `-p 8080:80`: Maps port 8080 on the host to port 80 in the container, making Nginx accessible via `http://localhost:8080`.
    - `nginx`: Specifies the image to use.

3. **Accessing the Nginx Web Server**:

    After running the container, you can access the default Nginx welcome page by navigating to `http://localhost:8080` in your web browser.

4. **Stopping and Removing the Nginx Container**:

    To stop the running Nginx container, use the following command:

    ```sh
    docker stop mynginx
    ```

    To remove the stopped container, use:

    ```sh
    docker rm mynginx
    ```

<br>

## 11. Push a Docker image from your local machine to Docker Hub

### 1. Create a Docker Hub Account

If you don't already have a Docker Hub account, you need to create one at [Docker Hub](https://hub.docker.com/).

### 2. Log In to Docker Hub

Log in to your Docker Hub account from the command line:

```sh
docker login
```

You will be prompted to enter your Docker Hub username and password.

### 3. Tag Your Local Image

Docker images need to be tagged with your Docker Hub username and repository name before they can be pushed. Assume you have a local image called `mydockercont:01`. You need to tag it as follows:

```sh
docker tag mydockercont:01 yourusername/mydockercont:01
```

Replace `yourusername` with your Docker Hub username.

### 4. Push the Image to Docker Hub

Use the `docker push` command to push your tagged image to Docker Hub:

```sh
docker push yourusername/mydockercont:01
```

<br>

## 12. Docker Volumes

Docker volumes are a way to persist data generated by and used by Docker containers. Volumes are stored outside of the container filesystem and can be shared and reused among containers.

### 🐳 Why Use Volumes?

- **Persistence**: Data is not lost when the container stops or is removed.
- **Sharing Data**: Volumes can be shared among multiple containers.
- **Performance**: Volumes are designed to be efficient and perform well with Docker.

### 🐳 Creating and Using Docker Volumes

#### 1. Creating a Volume

You can create a Docker volume using the `docker volume create` command:

```sh
docker volume create myvolume
```

#### 2. Using Volumes with Containers

You can use a volume when running a container by using the `-v` or `--mount` flag.

##### Using `-v` Flag

The `-v` flag allows you to bind a volume to a specific directory inside the container:

```sh
docker run -d --name mynginx -p 8080:80 -v myvolume:/usr/share/nginx/html nginx
```

In this example:
- `-d` runs the container in detached mode.
- `--name mynginx` names the container `mynginx`.
- `-p 8080:80` maps port 8080 on the host to port 80 in the container.
- `-v myvolume:/usr/share/nginx/html` mounts the `myvolume` volume to the `/usr/share/nginx/html` directory inside the container.


### 🐳 Managing Volumes

#### List Volumes

To list all Docker volumes, use:

```sh
docker volume ls
```

#### Inspect a Volume

To get detailed information about a volume, use:

```sh
docker volume inspect myvolume
```

#### Remove a Volume

To remove a volume, use:

```sh
docker volume rm myvolume
```

Note: You cannot remove a volume that is currently in use by any container.

<br>

## 12. Bind Mounts

Bind mounts allow you to mount a directory or file from the host machine into a container. This is useful for scenarios where you need the container to access or modify files on the host system, such as for development, testing, or running applications that need to read/write to the host file system.

### 🐳 Why Use Bind Mounts?

- **Development**: Quickly test changes without rebuilding the Docker image.
- **Data Sharing**: Share data between the host and containers.
- **Configuration**: Use host configuration files in containers.

### 🐳 Using Bind Mounts

To use a bind mount, you specify the path on the host machine and the path inside the container where the directory or file should be mounted.

Here's the syntax for running a Docker container with a bind mount using the `-v` flag:

```sh
docker run -v /path/to/local/file:/myapp/file imageid
```

### 🐳 Example

If you have a local file at `/home/user/myfile.txt` and you want to bind mount it to `/myapp/file.txt` inside the container, and your image ID is `5feb38d50bc3`, you would run:

```sh
docker run -v /home/user/myfile.txt:/myapp/file.txt 5feb38d50bc3
```

### 🐳 Explanation

- `docker run`: The base command to run a Docker container.
- `-v /path/to/local/file:/myapp/file`: The `-v` flag specifies the bind mount. The first part is the path to the local file, and the second part is the path inside the container where the file will be mounted.
- `imageid`: The ID or name of the Docker image to use.

### 🐳 Example with Nginx and Custom HTML File

1. **Create a Custom HTML File on the Host**

    ```sh
    mkdir -p ~/mynginx/html
    echo "<h1>Hello from Nginx with Bind Mount!</h1>" > ~/mynginx/html/index.html
    ```

2. **Run the Nginx Container with the Bind Mount**

    ```sh
    docker run -d --name mynginx -p 8080:80 -v ~/mynginx/html/index.html:/usr/share/nginx/html/index.html nginx
    ```

    This command:
    - Runs the container in detached mode (`-d`).
    - Names the container `mynginx` (`--name mynginx`).
    - Maps port 8080 on the host to port 80 in the container (`-p 8080:80`).
    - Binds the local file `~/mynginx/html/index.html` to `/usr/share/nginx/html/index.html` in the container (`-v ~/mynginx/html/index.html:/usr/share/nginx/html/index.html`).

3. **Access the Nginx Web Server**

    Open your web browser and navigate to `http://localhost:8080` to see the custom HTML content served by Nginx.

By using this syntax, you can easily share files between your host machine and Docker containers, enabling efficient development and testing workflows.

### 🐳 Managing Bind Mounts

Bind mounts are managed by the Docker daemon but are tied to the host file system. Unlike volumes, bind mounts do not persist data outside of the container lifecycle. However, they are useful for scenarios where real-time access to host files is required.

<br>

## 13. Docker Compose

Docker Compose is a tool that allows you to define and manage multi-container Docker applications. With Docker Compose, you can define the services that make up your app in a `docker-compose.yml` file and then run those services together with a single command.

Here’s a step-by-step example of using Docker Compose with a MERN (MongoDB, Express, React, Node.js) stack:

### Step 1: Set Up the Project Structure

Let's assume you have the following project structure:

```
mern-app/
  backend/
    Dockerfile
    server.js
    package.json
  frontend/
    Dockerfile
    src/
    public/
    package.json
  docker-compose.yml
```

### Step 2: Create Dockerfiles for Backend and Frontend

**Backend Dockerfile (`backend/Dockerfile`):**

```dockerfile
# Use the official Node.js image
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm install

# Bundle app source
COPY . .

# Bind to port 5000
EXPOSE 5000

# Run the app
CMD ["node", "server.js"]
```

**Frontend Dockerfile (`frontend/Dockerfile`):**

```dockerfile
# Use the official Node.js image
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm install

# Bundle app source
COPY . .

# Build the app
RUN npm run build

# Install serve to serve the build
RUN npm install -g serve

# Expose port 3000
EXPOSE 3000

# Serve the build
CMD ["serve", "-s", "build"]
```

### Step 3: Create a Docker Compose File

**Docker Compose file (`docker-compose.yml`):**

```yaml
version: '3.8'

services:
  frontend:
    build: 
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    depends_on:
      - backend

  backend:
    build: 
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "5000:5000"
    environment:
      - MONGODB_URI=mongodb+srv://pbarthwal90:Pranav123@cluster0.tx71i7y.mongodb.net
    depends_on:
      - mongo

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
```

### Step 4: Run Docker Compose

From the root of your project directory (`mern-app`), run the following command to start the services defined in your `docker-compose.yml` file:

```sh
docker-compose up --build
```

### Explanation of `docker-compose.yml`

- **version:** Specifies the version of the Docker Compose file format.
- **services:** Defines the different services that make up your application.

  - **frontend:** 
    - **build:** Specifies the build context and Dockerfile for the frontend service.
    - **ports:** Maps port 3000 on the host to port 3000 in the container.
    - **depends_on:** Specifies that the frontend service depends on the backend service.
  
  - **backend:** 
    - **build:** Specifies the build context and Dockerfile for the backend service.
    - **ports:** Maps port 5000 on the host to port 5000 in the container.
    - **environment:** Sets environment variables for the backend service.
    - **depends_on:** Specifies that the backend service depends on the mongo service.

  - **mongo:** 
    - **image:** Uses the official MongoDB image.
    - **ports:** Maps port 27017 on the host to port 27017 in the container.
    - **environment:** Sets environment variables for MongoDB.
