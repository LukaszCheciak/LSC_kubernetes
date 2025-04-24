# LSC Lab 6 Kubernetes

This repository contains a simple web application running in a Kubernetes cluster using Nginx and an NFS-backed volume. It demonstrates persistent storage and dynamic provisioning with Kubernetes.

## Requirements

Make sure you have the following tools installed:

- Docker
- kubectl
- kind
- Helm

## Setup Instructions

Follow these steps to set up and run the application.

### 1. Clone the Repository

```bash
git clone https://github.com/LukaszCheciak/LSC_kubernetes
cd LSC-LAB6
```

### 2. Create Kubernetes Cluster with kind

```bash
kind create cluster --name lsc-lab6 --config config.yaml
```

### 3. Install NFS Provisioner via Helm

```bash
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm repo update
helm install nfs-server nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --values values.yaml
```

### 4. Apply Kubernetes Manifests

Apply PVC:

```bash
kubectl apply -f pvc.yaml
```

Deploy web server:

```bash
kubectl apply -f deployment.yaml
```

Create service:

```bash
kubectl apply -f service.yaml
```

Run job to create HTML content:

```bash
kubectl apply -f job.yaml
```

### 5. Access the Application

Port-forward the service:

```bash
kubectl port-forward service/web-server-service 8080:80
```

Then open your browser and visit:

```
http://127.0.0.1:8080
```

You should see a simple "Hello World!!" web page.

