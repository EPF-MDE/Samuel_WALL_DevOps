# Samuel_WALL_DevOps
TP1

Question 1

Database Container Essentials
Dockerfile
The Dockerfile defines the configuration for building the Docker image.

Dockerfile
Copier le code
FROM postgres:14.1-alpine

ENV POSTGRES_DB=db \
    POSTGRES_USER=usr \
    POSTGRES_PASSWORD=pwd

COPY ./scripts_SQL/ /docker-entrypoint-initdb.d/
Commands
Build Docker Image
Use the following command to build the Docker image:

sh
Copier le code
docker build -t your_image_name .
Replace your_image_name with the desired name for your Docker image.

Run Docker Container
To run a Docker container based on the built image, execute the following command:

sh
Copier le code
docker run --name my_postgres_container --network app-network \
-e POSTGRES_DB=db -e POSTGRES_USER=usr -e POSTGRES_PASSWORD=pwd \
-d your_image_name
Replace my_postgres_container with the desired name for your container and your_image_name with the name of your Docker image.

Connect to the Database
To connect to the PostgreSQL database running inside the Docker container, execute the following command:

sh
Copier le code
docker exec -it my_postgres_container psql -U usr -d db
Replace my_postgres_container with the name of your container, usr with your PostgreSQL username, and db with your database name.


 Question 2

# Docker Multistage Build for Java Application

This document explains why a multistage build is used and provides a step-by-step explanation of the Dockerfile used to build and run a simplistic Java API.

## Why Use a Multistage Build?

A multistage build is used to create Docker images that are both efficient and small in size. This technique separates the build environment from the runtime environment, leading to several benefits:

1. **Reduced Image Size**: By including only the necessary runtime dependencies in the final image, the size of the image is significantly reduced, improving efficiency and security.
2. **Enhanced Security**: The build tools and intermediate files are not included in the final image, reducing the attack surface.
3. **Separation of Concerns**: Different stages can use different base images that are best suited for their respective purposes (e.g., a full JDK for building and a JRE for running).

## Dockerfile Explanation

The Dockerfile consists of two stages: the build stage and the run stage.

### Build Stage

```dockerfile
FROM maven:3.8.6-amazoncorretto-17 AS myapp-build

Question 3

# Docker Image Publication

This document provides the steps and commands used to tag and push Docker images to Docker Hub. It also lists the published images available in the Docker Hub repository.

## Prerequisites

- A Docker Hub account.
- Docker and Docker Compose installed on your machine.
- Docker images built locally (e.g., `my-database`, `my-backend`, `my-http-server`).

## Steps to Publish Docker Images

### 1. Log in to Docker Hub

Ensure you are logged in to Docker Hub. Use the following command and enter your Docker Hub username and password when prompted:

```sh
docker login