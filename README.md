# Production-Ready 3-Tier Web Application Deployment on Kubernetes

This repository contains the end-to-end DevOps implementation for hosting, scaling, and managing a secure 3-Tier Web Application using **Docker**, **Kubernetes (K8s)**, and configuration best practices.

---

## 🏗️ Architecture Overview

The application follows a standard three-tier architecture design to ensure high availability, security, and separation of concerns:

1. **Presentation Tier (Frontend):** Built with React/HTML, served via Nginx. It communicates with the backend API.
2. **Logic Tier (Backend):** Built with Node.js/Express (or Python Flask) API handling database operations.
3. **Data Tier (Database):** Secure MongoDB/MySQL instance utilizing Kubernetes Persistent Volumes for data preservation.

---

## 🛠️ Tech Stack & DevOps Tools
* **Containerization:** Docker & Docker Compose
* **Orchestration:** Kubernetes (K8s)
* **Web Server/Reverse Proxy:** Nginx
* **Configuration Management:** K8s ConfigMaps & Secrets

---

## 📁 Repository Structure

```bash
├── .github/workflows/    # CI/CD pipelines (Optional/Future)
├── frontend/             # Frontend source code & Dockerfile
├── backend/              # Backend source code & Dockerfile
├── k8s-manifests/        # Kubernetes Deployment & Service files
│   ├── database-pvc.yaml # Persistent Volumes for DB storage
│   ├── database-secret.yaml # Encrypted Database credentials
│   ├── database.yaml     # DB Deployment & ClusterIP Service
│   ├── backend.yaml      # Backend Deployment & ClusterIP Service
│   ├── frontend.yaml     # Frontend Deployment & NodePort/LoadBalancer Service
└── README.md             # Project documentation
```

---

## 🚀 Step-by-Step Deployment Guide

### Phase 1: Local Containerization (Docker)
First, build and test the containers locally to ensure environment consistency.

1. **Build and run the entire stack locally using Docker Compose:**
   ```bash
   docker-compose up --build -d
   ```
2. Check if all containers are running successfully:
   ```bash
   docker ps
   ```

### Phase 2: Kubernetes Orchestration
Once the images are verified, deploy the application onto your Kubernetes cluster (Minikube / EKS / K3s).

1. **Apply Infrastructure Configurations (Secrets & Storage):**
   ```bash
   kubectl apply -f k8s-manifests/database-secret.yaml
   kubectl apply -f k8s-manifests/database-pvc.yaml
   ```

2. **Deploy the Database Layer:**
   ```bash
   kubectl apply -f k8s-manifests/database.yaml
   ```

3. **Deploy the Logic/Backend Layer:**
   ```bash
   kubectl apply -f k8s-manifests/backend.yaml
   ```

4. **Deploy the Presentation/Frontend Layer:**
   ```bash
   kubectl apply -f k8s-manifests/frontend.yaml
   ```

---

## 🔍 Verification & Accessing the App

1. **Verify all components are active and healthy:**
   ```bash
   kubectl get pods,svc,pvc
   ```

2. **Access the application:**
   * If using **Minikube**, run the following command to get the external URL for the frontend:
     ```bash
     minikube service frontend-service --url
     ```

---

## 🌟 Implemented DevOps Best Practices
* **Data Persistence:** Used Kubernetes `PersistentVolumeClaim` (PVC) to prevent data loss when database pods restart.
* **Security & Hardening:** Decoupled database passwords from code using encrypted Kubernetes `Secrets`.
* **Zero Downtime Updates:** Utilized Kubernetes rolling updates strategy for seamless application rollouts.
* **Service Discovery:** Implemented `ClusterIP` services for secure internal pod-to-pod communication.

---
💡 *Developed by a Passionate Cloud & DevOps Engineer focused on infrastructure automation.*
