# Flask K8s CI/CD Pipeline Assignment

A complete CI/CD pipeline for a Flask application with automated testing, Docker containerization, and Kubernetes deployment.

## Project Overview

This project demonstrates a production-ready DevOps workflow using:
- **Flask**: Python web application
- **GitHub Actions**: Automated CI with testing and linting
- **Docker**: Container packaging
- **Kubernetes**: Orchestration with minikube
- **Jenkins**: CD pipeline for automated deployment

## Features

### Kubernetes Features
- **Rolling Updates**: Zero-downtime deployments with maxSurge=1, maxUnavailable=1
- **Auto-scaling**: 3 replicas for high availability
- **Load Balancing**: NodePort service distributing traffic across pods
- **Resource Management**: CPU and memory limits/requests configured

## Local Development

### Prerequisites
- Docker
- Python 3.9+
- kubectl
- minikube

### Build and Run with Docker
```bash
# Build image
docker build -t flask-app:latest .

# Run container
docker run -p 5000:5000 flask-app:latest

# Access at http://localhost:5000
```

## Kubernetes Deployment

### Using Jenkins Pipeline

1. Start minikube: `minikube start`
2. Access Jenkins: `http://localhost:8080`
3. Run the `flask-k8s-pipeline` job
4. Pipeline will:
   - Build Docker image
   - Deploy to Kubernetes
   - Verify deployment status

### Manual Deployment
```bash
# Load image to minikube
minikube image load flask-app:latest

# Apply manifests
kubectl apply -f kubernetes/

# Check status
kubectl get pods,services,deployments

# Access application
minikube service flask-service
```

### Scaling
```bash
# Scale up
kubectl scale deployment flask-app --replicas=5

# Scale down
kubectl scale deployment flask-app --replicas=3
```

### Rollback
```bash
kubectl rollout undo deployment/flask-app
kubectl rollout status deployment/flask-app
```

## CI/CD Pipeline

- **GitHub Actions**: Runs on every push
  - Flake8 linting (max 90 chars)
  - Pytest unit tests
  - Docker build

- **Jenkins**: Deploys on merge to main
  - Builds Docker image
  - Deploys to Kubernetes
  - Verifies deployment

## Contributors

- Admin: Muhammad Zain Ali
- Developer: Ibrahim Ansari
