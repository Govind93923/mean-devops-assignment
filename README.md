# MEAN Stack CRUD Application Deployment

This repository contains a *full-stack MEAN (MongoDB, Express.js, Angular, Node.js) CRUD application, containerized using Docker, orchestrated with Docker Compose, and deployed to an **AWS EC2 instance* using *CI/CD via GitHub Actions*.

---

## ⚙ Project Components

* *Frontend:* Angular
* *Backend:* Node.js with Express.js
* *Database:* MongoDB
* *Web Server & Reverse Proxy:* Nginx
* *CI/CD:* GitHub Actions
* *Deployment:* Docker, Docker Compose on AWS EC2

---

## 🐳 Docker Configuration

### Backend Dockerfile

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
Frontend Dockerfile
Dockerfile

FROM node:18 as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build --prod

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
Docker Compose File (docker-compose.yml)
YAML

version: '3.8'
services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  frontend:
    build: ./frontend
    ports:
      - "80:80"
  
  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
🚀 CI/CD with GitHub Actions
The following workflow is located at .github/workflows/deploy.yml.

YAML

name: Deploy to EC2

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Set up SSH
      uses: webfactory/ssh-agent@v0.5.3
      with:
        ssh-private-key: ${{ secrets.EC2_SSH_KEY }}

    - name: Deploy to EC2
      run: |
        ssh -o StrictHostKeyChecking=no ubuntu@${{ secrets.EC2_PUBLIC_IP }} \
        'cd ~/mean-app && git pull && docker-compose down && docker-compose up -d --build'
🌐 Nginx Configuration
The nginx.conf file, located in the nginx/ directory, is used to serve the frontend.

Nginx

events {}
http {
    server {
        listen 80;
        location / {
            root /usr/share/nginx/html;
            index index.html;
            try_files $uri $uri/ /index.html;
        }
    }
}
📋 Deployment Instructions
Clone the repository on your EC2 instance:

Bash

git clone <your-repo-url>
cd mean-app
Start the application with Docker Compose:

Bash

docker-compose up -d --build
Access the application:
Open your web browser and navigate to http://<EC2_PUBLIC_IP>.

📸 Screenshots
CI/CD Execution:

Application UI:

📈 Future Improvements
Add SSL with Let's Encrypt.

Implement auto-scaling with AWS ECS.

Set up centralized logging with the ELK Stack.
