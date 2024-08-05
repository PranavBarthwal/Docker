# This is a sample Dockerfile to create a Docker image with Node.js installed.

# Base image : here we are using node base image, we can also mention specific version of node image
FROM node:20

# Working directory : setting to /myapp (will create a directory in container)
WORKDIR /myapp

# Copying all files from current directory to /myapp directory in container
COPY . .

# Installing all dependencies
RUN npm install

# Exposing the port 3000
EXPOSE 3000

# running the application 
CMD ["npm", "start"]



# Build the Docker image : Run the following command to build the Docker image.
# docker build .

# check the image is created or not : Run the following command to check if the Docker image is created.
# docker images ls

# Run the Docker image : Run the following command to run the Docker image.
    # 1. with binding the port 3000 of the container to the port 3000 of the host machine
    #docker run -p 3000:3000 <image_id>

    # 2.without binding the port
    # docker run <image_id>

# launch new terminal and run the following command to check the running container.
# docker ps

# Stop the Docker container : Run the following command to stop the Docker container.
# docker stop <name>

