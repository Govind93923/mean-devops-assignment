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

![WhatsApp Image 2025-08-24 at 22 49 58_dc4f397c](https://github.com/user-attachments/assets/728807fa-e48e-43bc-a5e3-177d8ee986fa)
<img width="1919" height="873" alt="Screenshot 2025-08-24 225044" src="https://github.com/user-attachments/assets/2eb64de5-fb2f-4073-a6ae-1531cff7deb0" />

<img width="1919" height="258" alt="Screenshot 2025-08-24 224220" src="https://github.com/user-attachments/assets/5cc563b1-a6b2-4881-8c1a-c7533792df00" />
<img width="1913" height="494" alt="Screenshot 2025-08-24 224333" src="https://github.com/user-attachments/assets/e33fae60-50c8-48c7-b8b1-d44479288236" />
<img width="1919" height="744" alt="Screenshot 2025-08-24 224946" src="https://github.com/user-attachments/assets/d0849f1d-f371-43ad-ba26-4418c7e2968a" />
<img width="1919" height="773" alt="Screenshot 2025-08-24 224703" src="https://github.com/user-attachments/assets/ea47f355-13d1-4f53-9471-0a19a45bafc1" />


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
