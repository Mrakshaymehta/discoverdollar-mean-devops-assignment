# 🚀 MEAN Stack DevOps Deployment Assignment

This project demonstrates containerization, CI/CD implementation, and VM-based deployment of a full-stack MEAN (MongoDB, Express, Angular, Node.js) application.

---

# 📌 Project Overview

The application is a CRUD-based MEAN stack project that has been:

- ✅ Containerized using Docker
- ✅ Deployed using Docker Compose
- ✅ Hosted on Ubuntu VM (VirtualBox)
- ✅ Integrated with MongoDB (Dockerized)
- ✅ Reverse proxied using Nginx
- ✅ Automated with GitHub Actions CI/CD pipeline
- ✅ Docker images pushed to Docker Hub

---

# 🏗️ Architecture

GitHub → GitHub Actions → Docker Hub → Ubuntu VM → Docker Compose → Nginx → Frontend + Backend + MongoDB

---

# 🐳 Docker Setup

## Backend
- Base Image: Node 18 Alpine
- Production dependencies installed
- Runs Express server on port 8080

## Frontend
- Multi-stage Docker build
- Angular production build
- Served via Nginx

## MongoDB
- Official MongoDB Docker image
- Persistent Docker volume storage

---

# 📦 Docker Hub Images

Backend Image:
https://hub.docker.com/r/mrakshaymehta/backend

Frontend Image:
https://hub.docker.com/r/mrakshaymehta/frontend

---

# 🖥️ Ubuntu VM Deployment (VirtualBox)

## VM Configuration
- OS: Ubuntu 22.04 ARM64
- RAM: 4GB
- CPU: 2 cores
- Disk: 25GB
- Network: Bridged Adapter

---

# 🚀 Deployment Steps on VM

## 1️⃣ Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

## 2️⃣ Install Docker Compose

```bash
sudo apt install docker-compose -y
```

## 3️⃣ Run Application

```bash
docker-compose up -d
```

Application accessible at:

http://<VM_IP>

---

# 🌐 Nginx Reverse Proxy

Nginx is configured as a reverse proxy:

- Port 80 exposed publicly
- Routes `/` → Frontend
- Routes `/api` → Backend

Example Nginx Configuration:

```nginx
events {}

http {
    server {
        listen 80;

        location / {
            proxy_pass http://frontend:80;
        }

        location /api/ {
            proxy_pass http://backend:8080/;
        }
    }
}
```

---

# 🔄 CI/CD Pipeline (GitHub Actions)

The pipeline automatically:

1. Builds Docker images on every push to main
2. Pushes updated images to Docker Hub
3. SSH into Ubuntu VM
4. Pulls latest images
5. Restarts containers using Docker Compose

Workflow file location:

.github/workflows/deploy.yml

---

# 📁 Project Structure

```
.
├── backend/
│   ├── Dockerfile
├── frontend/
│   ├── Dockerfile
├── docker-compose.yml
├── nginx.conf
├── .github/workflows/deploy.yml
└── README.md
```

---

# 📸 Screenshots

Included screenshots in `/screenshots` folder:

- GitHub Actions successful run
- Docker image build logs
- Docker Hub repositories
- Running containers (`docker ps`)
- Application UI
- Nginx configuration
- VM infrastructure details

---

# 🔒 Notes

- Infrastructure is kept active for demonstration.
- MongoDB data is persisted using Docker volumes.
- Deployment is fully automated through CI/CD.
- Application is accessible via port 80 through Nginx reverse proxy.

---

# ✅ Assignment Completion Checklist

✔ GitHub repository created  
✔ Dockerfiles for frontend & backend  
✔ Docker Compose configuration  
✔ MongoDB Docker setup  
✔ Ubuntu VM deployment  
✔ Nginx reverse proxy  
✔ CI/CD automation  
✔ Docker Hub integration  
✔ Documentation with screenshots  

---

# 👨‍💻 Author

Akshay Mehta  
DevOps Internship Assignment Submission
