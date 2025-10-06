# Next.js DevOps Assessment

## Overview
Containerized Next.js application, built and deployed using Docker, GitHub Actions, and Kubernetes (Minikube).

## Setup

### Local Development

```bash
npm install
npm run dev
```

### Build & Run Docker Locally

```bash
docker build -t nextjs-app .
docker run -p 3000:3000 nextjs-app
```

### Using GHCR Image

Replace `<your-github-username>/<your-repo-name>` with your details:

```bash
docker run -p 3000:3000 ghcr.io/<your-github-username>/<your-repo-name>:latest
```

## GitHub Actions Workflow

- On push to `main`, builds and pushes Docker image to GHCR.

## Kubernetes (Minikube) Deployment

```bash
minikube start
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl get pods
kubectl get svc
```

Access the app via:

```bash
minikube service nextjs-service
```

## Health Checks

- Readiness and liveness probes configured in deployment manifest.

## Useful Links

- [GHCR Image URL](https://ghcr.io/<your-github-username>/<your-repo-name>)
- [Repository URL](https://github.com/<your-github-username>/<your-repo-name>)