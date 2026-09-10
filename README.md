# 🚀 End-to-End CI/CD Deployment on Amazon EKS

## 📌 Project Overview

This project demonstrates an end-to-end DevOps workflow for deploying a containerized application on Amazon EKS using Jenkins, Docker, GitHub, and Kubernetes.

The project covers:

- Source code management using GitHub
- CI/CD automation using Jenkins
- Docker image creation and publishing
- Kubernetes deployment on Amazon EKS
- Application exposure using a LoadBalancer
- Kubernetes rolling updates
- Pod self-healing
- EKS worker node recovery

## 🏗️ Project Architecture

```text
Developer
    │
    ▼
  GitHub
    │
    ▼
 Jenkins on EC2
    │
    ├── Build Docker Image
    │
    └── Push Image
          │
          ▼
      Docker Hub
          │
          ▼
      Amazon EKS
          │
          ▼
   Kubernetes Deployment
          │
          ▼
    Worker Node(s)
          │
          ▼
   Kubernetes Service
      LoadBalancer
          │
          ▼
     Application
```


## Technologies Used
- AWS
- Amazon EKS
- Amazon EC2
- IAM
- Jenkins
- Docker
- Kubernetes
- GitHub
- Docker Hub

## 🔄 CI/CD Pipeline

The project uses Jenkins to automate the application build and deployment process.

### Pipeline Flow

1. Developer pushes code to GitHub.
2. Jenkins detects the code change through a GitHub webhook.
3. Jenkins pulls the latest source code.
4. Jenkins builds the Docker image.
5. The Docker image is tagged with the Jenkins build number.
6. Jenkins pushes the image to Docker Hub.
7. Jenkins updates the Kubernetes deployment with the new image.
8. Kubernetes performs a rolling update of the application pods.
9. The updated application is exposed through a Kubernetes LoadBalancer.

### CI/CD Workflow

```text
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
Docker Hub
   ↓
Amazon EKS
   ↓
Kubernetes Deployment
   ↓
Rolling Update
   ↓
Application
