# LSC Lab 6 - Kubernetes Application with NFS Storage

This repository contains configuration files for creating a Kubernetes application that demonstrates persistent storage using NFS.

## Setup Instructions

Follow these steps to run the application:

1. Create a kind cluster:
   ```bash
   kind create cluster --name lsc-lab6 --config kind-config.yaml
   ```

2. Install the NFS server and provisioner:
   ```bash
   helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
   helm repo update
   helm install nfs-server nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --values nfs-values.yaml
   ```

3. Apply Kubernetes resources:
   ```bash
   kubectl apply -f pvc.yaml
   kubectl apply -f nginx-deployment.yaml
   kubectl apply -f service.yaml
   kubectl apply -f content-job.yaml
   ```

4. Access the application:
   ```bash
   kubectl port-forward service/web-server-service 8080:80
   ```
   Then open http://localhost:8080 in your browser.