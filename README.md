Docker 2-Tier Flask App Deployment
Introduction
This project aims to deploy a 2-tier Flask application using Docker. The application consists of a frontend Flask app and a backend database. The Docker infrastructure allows for easy deployment, scalability, and data persistence.

Dockerfile
Base Image Dockerfile FROM ubuntu:latest ENV HTTP_PORT="9000" WORKDIR /app
