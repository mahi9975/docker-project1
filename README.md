---

# Docker 2-Tier Flask App Deployment

## Introduction

This project facilitates the deployment of a 2-tier Flask application using Docker. The application consists of a frontend Flask app and a backend database. Docker infrastructure ensures easy deployment, scalability, and data persistence.

## Dockerfile

### Base Image

```Dockerfile
FROM ubuntu:latest
ENV HTTP_PORT="5000"
WORKDIR /app
```

### Install Dependencies

```Dockerfile
RUN apt-get update && \
    apt-get install -y python3 python3-pip
```

### Copy Application Code

```Dockerfile
COPY . /app
```

### Set Entrypoint and CMD

```Dockerfile
ENTRYPOINT ["sh", "-c", "python3 app.py"]
CMD ["--port", "$HTTP_PORT"]
```

## Docker Compose

### Services

#### Flask App

```bash
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - ./app:/app
    networks:
      - mynetwork
```

#### Database

```bash
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: test@123
    volumes:
      - ./data:/var/lib/mysql
    networks:
      - mynetwork
```

### Networks

```bash
networks:
  mynetwork:
    driver: bridge
```

## Docker Hub

1. Create a Docker Hub account: [Docker Hub](https://hub.docker.com/)
2. Check Docker images:

```bash
docker images
```

3. Log in to Docker Hub:

```bash
docker login
```

4. Tag your image with your Docker Hub username:

```bash
docker tag flask-app:latest <username>/flask-app
```

5. Push your images to Docker Hub:

```bash
docker push <username>/flask-app
```

## Docker Volumes

Store data persistently even after container deletion:

```bash
docker run -d -v $(pwd):/var/lib/mysql --name mysql -e MYSQL_ROOT_PASSWORD=test@123 mysql:5.7
```

## Docker Networks

Explore various types of Docker networks:

- Bridge Network
- Default Network
- Macvlan Network
- IPvlan Networking
- User Default
- Host Network
- Overlay Network

## Multi-Tier Application

Deploy a multi-tier application with a database using Docker.

## Multi-Stage Docker Build

Compress your Docker image size from 1GB to 200MB using multi-stage builds.

## Docker Scout (DevSecOps)

Leverage Docker Scout for DevSecOps and continuous integration.

## Docker Compose

Use Docker Compose to simplify multi-container deployments.

---

Feel free to further customize this README file based on the specific details of your project, including additional information about your Flask app, database schema, and any other configurations necessary for your deployment.
