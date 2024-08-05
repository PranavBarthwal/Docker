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




