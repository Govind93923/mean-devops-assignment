# MEAN Stack CRUD Application Deployment

This repository contains a *full-stack MEAN (MongoDB, Express.js, Angular, Node.js) CRUD application, containerized using Docker, orchestrated with Docker Compose, and deployed to an **AWS EC2 instance* using *CI/CD via GitHub Actions*.

---

## Project Overview

This project demonstrates a complete DevOps workflow for deploying a full-stack application.

* *Frontend:* Angular
* *Backend:* Node.js with Express.js
* *Database:* MongoDB
* *Web Server & Reverse Proxy:* Nginx
* *Containerization:* Docker & Docker Compose
* *CI/CD:* GitHub Actions
* *Deployment Environment:* AWS EC2 (Ubuntu)

---

## Docker Configuration

*Backend Dockerfile*: This Dockerfile builds the Node.js backend application. It starts with a base Node.js image, sets the working directory, copies the package files, installs dependencies, and then copies the source code. The final CMD command runs the application using npm start.

*Frontend Dockerfile*: This file uses a multi-stage build to handle the Angular frontend. The first stage uses a Node.js image to build the Angular application, which compiles the project into static files. The second stage uses a lightweight Nginx image to serve these static files, ensuring a small and efficient final image for production.

---

## CI/CD with GitHub Actions

The GitHub Actions workflow is defined in a YAML file. It's triggered on a push to the main branch. The job checks out the repository's code, sets up an SSH connection to the AWS EC2 instance using a private key stored as a GitHub secret, and then executes a single SSH command on the remote server. This command navigates to the project directory, pulls the latest code from the repository, and runs a command to stop and restart the containers in detached mode, using new images.

---

## Nginx Configuration

The nginx.conf file is a reverse proxy configuration that routes incoming web traffic. It listens on port 80 and serves the Angular frontend's static files. The try_files directive is crucial for single-page applications (SPAs) like Angular, as it ensures that all deep links are redirected to the index.html file, allowing Angular's routing to handle the navigation on the client side.

---

## Deployment Steps

1. *Clone the repository on EC2:*
git clone <repo_url>
cd mean-app
2. *Start the application using Docker Compose:*
docker-compose up -d --build
3. *Access the app:* http://<EC2_PUBLIC_IP>

---

## Screenshots

* *CI/CD Execution:* (Attach GitHub Actions screenshot)
* *Application UI:* (Attach running app screenshot)

---

## Conclusion

This setup ensures *seamless CI/CD pipeline integration, a **containerized environment, and **scalable deployment* of a MEAN application on AWS.

---

## Future Improvements

* Add *SSL with Let's Encrypt*.
* Implement *auto-scaling with AWS ECS*.
* Set up *centralized logging with the ELK Stack*.
