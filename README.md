This repository contains a full-stack MEAN (MongoDB, Express.js, Angular, Node.js) CRUD application, containerized using Docker, orchestrated with Docker Compose, and deployed to an AWS EC2 instance using CI/CD via GitHub Actions.

📌 Project Overview

This project demonstrates a complete DevOps workflow for deploying a full-stack application.

Frontend: Angular

Backend: Node.js with Express.js

Database: MongoDB

Web Server & Reverse Proxy: Nginx

Containerization: Docker & Docker Compose

CI/CD: GitHub Actions

Deployment Environment: AWS EC2 (Ubuntu)

🏗️ Architecture Diagram

Here’s the high-level architecture of this project:

                ┌────────────────────────┐
                │      Developer         │
                │ (Push code to GitHub)  │
                └──────────┬─────────────┘
                           │
                           ▼
                ┌────────────────────────┐
                │   GitHub Actions CI/CD │
                │ - Build Docker images  │
                │ - SSH to EC2           │
                │ - Deploy containers    │
                └──────────┬─────────────┘
                           │
                           ▼
         ┌───────────────────────────────────────┐
         │            AWS EC2 (Ubuntu)           │
         │                                       │
         │   ┌───────────┐   ┌──────────────┐    │
         │   │  Angular  │   │   Node.js     │    │
         │   │ Frontend  │◄──►│ Express API  │    │
         │   └───────────┘   └──────────────┘    │
         │          ▲                 │           │
         │          │                 ▼           │
         │   ┌──────────────┐   ┌──────────────┐ │
         │   │   Nginx RP   │   │   MongoDB    │ │
         │   └──────────────┘   └──────────────┘ │
         └───────────────────────────────────────┘


Developer pushes code → GitHub Actions triggers.

CI/CD pipeline builds & deploys containers to AWS EC2.

Nginx acts as a reverse proxy → routes traffic to Angular & Node.js backend.

MongoDB stores application data.

⚙️ Docker Configuration

Backend Dockerfile

Builds the Node.js backend application.

Uses Node.js base image.

Installs dependencies.

Copies source code.

Runs the app with npm start.

Frontend Dockerfile

Multi-stage build for Angular.

Stage 1: Builds Angular app into static files.

Stage 2: Uses Nginx to serve static files.

Ensures optimized, lightweight production-ready image.

🔄 CI/CD with GitHub Actions

Workflow defined in .github/workflows/deploy.yml.

Trigger: push to main branch.

Steps:

Checkout repository code.

Establish SSH connection to AWS EC2 (using GitHub Secrets).

Pull latest code on EC2.

Restart containers with docker-compose up -d --build.

🌐 Nginx Configuration

Reverse proxy configuration (nginx.conf).

Routes incoming traffic to Angular frontend & backend API.

SPA Handling: try_files ensures deep links redirect to index.html.

🚀 Deployment Steps

Clone the repository on EC2

git clone <repo_url>
cd mean-app


Start the application using Docker Compose

docker-compose up -d --build
📸 Screenshots
1. Application Running on Browser
2. Angular Frontend UI
<img width="1919" height="873" alt="Frontend UI" src="https://github.com/user-attachments/assets/2eb64de5-fb2f-4073-a6ae-1531cff7deb0" />
<img width="1919" height="258" alt="MongoDB Data" src="https://github.com/user-attachments/assets/5cc563b1-a6b2-4881-8c1a-c7533792df00" />
<img width="1913" height="494" alt="Backend Logs" src="https://github.com/user-attachments/assets/e33fae60-50c8-48c7-b8b1-d44479288236" />
<img width="1919" height="744" alt="Docker Running" src="https://github.com/user-attachments/assets/d0849f1d-f371-43ad-ba26-4418c7e2968a" />
<img width="1919" height="773" alt="GitHub Actions CI/CD" src="https://github.com/user-attachments/assets/ea47f355-13d1-4f53-9471-0a19a45bafc1" />
✅ Conclusion

This setup ensures:

Seamless CI/CD integration with GitHub Actions.

Containerized environment using Docker & Docker Compose.

Scalable deployment on AWS EC2.

🔮 Future Improvements

Add SSL with Let’s Encrypt.

Implement auto-scaling with AWS ECS.

Set up centralized logging with ELK Stack.
