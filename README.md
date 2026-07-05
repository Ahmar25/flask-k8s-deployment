# Flask App on Kubernetes — End-to-End Deployment
A small Flask app containerized with Docker and deployed to a local
Kubernetes cluster (minikube), demonstrating self-healing and scaling.

## Stack
- Flask (Python)
- Docker (multi-stage-ready build)
- Kubernetes (Deployment + Service, liveness/readiness probes)
- minikube (local cluster)

## What this demonstrates
- Building and running a containerized app
- Deploying to Kubernetes with 2 replicas
- Health checks via liveness/readiness probes
- Self-healing: deleting a pod triggers automatic recreation
- Manual scaling (2 → 4 replicas)

## How to run
***bash
docker build -t myapp:v1 .
minikube start
eval $(minikube docker-env)      # or: minikube docker-env | Invoke-Expression (PowerShell)
docker build -t myapp:v1 .
kubectl apply -f deployment.yaml
minikube service myapp-service

## Self-healing demo
***bash
kubectl get pods
kubectl delete pod <pod-name>
kubectl get pods -w   # watch Kubernetes recreate it automatically
