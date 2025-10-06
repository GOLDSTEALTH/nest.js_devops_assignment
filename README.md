# DevOps Internship Assessment - Next.js Application

## Objective

Containerize and deploy a Next.js application using Docker, GitHub Actions, and Minikube.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Local Development](#local-development)
- [Docker](#docker)
- [GitHub Actions & GHCR](#github-actions--ghcr)
- [Kubernetes (Minikube) Deployment](#kubernetes-minikube-deployment)
- [Accessing the Application](#accessing-the-application)
- [Repository & Image URLs](#repository--image-urls)

---

## Project Overview

This repo demonstrates:
- Containerizing a Next.js app with Docker
- Automated CI/CD pipeline using GitHub Actions
- Pushing container images to GitHub Container Registry (GHCR)
- Deploying the container to Kubernetes (Minikube)
- Exposing the app via a Kubernetes Service

---

## Prerequisites

- [Node.js](https://nodejs.org/) & [npm](https://www.npmjs.com/)
- [Docker](https://www.docker.com/)
- [GitHub account](https://github.com/)
- [Minikube](https://minikube.sigs.k8s.io/docs/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

---

## Local Development

1. **Install dependencies:**
   ```sh
   npm install
   ```

2. **Start the Next.js app:**
   ```sh
   npm run dev
   ```
   App runs at [http://localhost:3000](http://localhost:3000)

---

## Docker

1. **Build Docker image:**
   ```sh
   docker build -t ghcr.io/GOLDSTEALTH/nest_js_devops_assignment:latest .
   ```

2. **Run the container:**
   ```sh
   docker run -p 3000:3000 ghcr.io/GOLDSTEALTH/nest_js_devops_assignment:latest
   ```

---

## GitHub Actions & GHCR

- On push to `main`, [GitHub Actions](.github/workflows/) will:
  - Build the Docker image
  - Tag and push to GHCR

**GHCR Image URL:**  
```
ghcr.io/GOLDSTEALTH/nest_js_devops_assignment:latest
```

---

## Kubernetes (Minikube) Deployment

1. **Start Minikube:**
   ```sh
   minikube start
   ```

2. **Apply manifests:**
   ```sh
   kubectl apply -f k8s/deployment.yml
   kubectl apply -f k8s/service.yml
   ```

3. **Check pod status:**
   ```sh
   kubectl get pods
   ```

4. **Check service status:**
   ```sh
   kubectl get services
   ```

---

## Accessing the Application

### Option 1: Using Minikube Service Command

Run:
```sh
minikube service nextjs-service
```
Minikube will open a browser tab or output a URL like:
```
http://127.0.0.1:64852/
```
Use this IP and port to access your app locally.

### Option 2: Using Minikube IP and NodePort

1. **Get Minikube IP:**
   ```sh
   minikube ip
   ```
   Example: `192.168.49.2`

2. **Find NodePort for your service:**
   ```sh
   kubectl get services
   ```
   Example: `nextjs-service` at port `32000`

3. **Access in browser:**  
   ```
   http://<minikube_ip>:<nodeport>
   ```
   Example: [http://192.168.49.2:32000](http://192.168.49.2:32000)

---

## Repository & Image URLs

- **Repo URL:** [https://github.com/GOLDSTEALTH/nest.js_devops_assignment](https://github.com/GOLDSTEALTH/nest.js_devops_assignment)
- **GHCR Image URL:**  
  ```
  ghcr.io/GOLDSTEALTH/nest_js_devops_assignment:latest
  ```

---

## Additional Notes

- See [k8s/deployment.yml](k8s/deployment.yml) and [k8s/service.yml](k8s/service.yml) for deployment configuration.
- Health checks are configured for readiness and liveness probes.
- For troubleshooting, use:
  ```sh
  kubectl describe pod <pod-name>
  kubectl logs <pod-name>
  ```

---

## License

MIT