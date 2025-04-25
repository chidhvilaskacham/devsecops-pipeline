## Kubernetes Deployment for Tic Tac Toe on Kind

This directory contains Kubernetes manifests for deploying the Tic Tac Toe application.

## Components 
1. Deployment: Manages the application pods with scaling and update strategies
2. Service: Exposes the application within the cluster

## Prerequisites
1. Kind: Install Kind
2. kubectl: Install kubectl
3. Docker: Install Docker
4. Container registry access (GitHub Container Registry in this case)Setup

## 1.  Create a Kind Cluster
    If you don't have a Kind cluster running, create one:

```bash
kind create cluster --name tic-tac-toe-cluster
```

Verify that your cluster is running:

```bash
kubectl cluster-info --context kind-tic-tac-toe-cluster

```
## 2.  Install Argo CD
    To install Argo CD in your Kind cluster, follow these steps:

* **Create the Argo CD namespace:**

    ```bash
    kubectl create namespace argocd
    ```

* **Apply the Argo CD installation manifests:**

    ```bash
    kubectl apply -n argocd -f [https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml](https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml)
    ```

* **Port forward to the Argo CD server:**

    To access the Argo CD UI, you need to forward a port from your local machine to the Argo CD server within the cluster:

    ```bash
    kubectl port-forward svc/argocd-server -n argocd 80:443
    ```

    Now, you can access the Argo CD UI in your browser at `https://localhost:80`.  You might need to accept a self-signed certificate warning.

* **Get the Argo CD admin password:**

    The initial password for the `admin` user is stored in a Kubernetes secret.  Retrieve it with:

    ```bash
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
    ```

    Use this password to log in to the Argo CD UI.  It is highly recommended that you change this password after your first login.

## 3.  Create a Kubernetes Secret
  Create a secret to allow your Kind cluster to pull the image from GitHub Container Registry.

```bash
kubectl create secret docker-registry github-container-registry \\
  --docker-server=ghcr.io \\
  --docker-username=YOUR_GITHUB_USERNAME \\
  --docker-password=YOUR_GITHUB_TOKEN \\
  --docker-email=YOUR_EMAIL

```

Replace `YOUR_GITHUB_USERNAME`, `YOUR_GITHUB_TOKEN`, and `YOUR_EMAIL` with your actual GitHub credentials.

## Port Forwarding  

```bash
kubectl port-forward service/tic-tac-toe-service 8080:80

```
You can then access the application in your browser at `http://localhost:8080`.

