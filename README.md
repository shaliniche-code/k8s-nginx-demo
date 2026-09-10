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
```

## ☸️ Kubernetes Deployment

The application is deployed on an Amazon EKS cluster using Kubernetes manifests.

### Kubernetes Resources

- **Deployment** – Manages the application pods and maintains 3 replicas.
- **Service** – Exposes the application using an AWS LoadBalancer.
- **Pods** – Run the containerized NGINX application on the EKS worker node.
- **Worker Node** – Provides the compute capacity for running the application.

### Deployment Configuration

The Kubernetes Deployment is configured with:

- Replicas: 3
- Application: NGINX
- Container image: Docker image stored in Docker Hub
- Service type: LoadBalancer

### Rolling Update

When a new Docker image is deployed, Kubernetes gradually replaces the existing pods with new pods.

This allows the application to be updated without bringing down all replicas at the same time.

## 🧪 Testing & Self-Healing

The Kubernetes deployment was tested to verify application availability and automatic recovery.

### 1. Pod Self-Healing

A running application pod was manually deleted to test Kubernetes self-healing.

**Result:**

Kubernetes automatically created a replacement pod to maintain the desired replica count.

```text
Before:
Pod 1    Pod 2    Pod 3
  ✓        ✓        ✓

Delete Pod 2
       ↓

Kubernetes detects missing replica
       ↓

New Pod created
       ↓

Pod 1    Pod 2    Pod 3
  ✓        ✓        ✓
```

## 2. Worker Node Recovery

The EKS worker node was manually terminated to test node recovery.

The managed node group was configured with:

- Minimum nodes: 1
- Maximum nodes: 2

## Result:

After the worker node was terminated, EKS automatically provisioned a replacement worker node to maintain the required capacity.

## 3. Rolling Update Verification

The application deployment was updated and the Kubernetes rollout was monitored.

## Result:

The existing pods were gradually replaced with the updated pods, demonstrating a Kubernetes rolling update without requiring all replicas to be stopped simultaneously.
