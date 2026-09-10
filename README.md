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


##Technologies Used
- AWS
- Amazon EKS
- Amazon EC2
- IAM
- Jenkins
- Docker
- Kubernetes
- GitHub
- Docker Hub
