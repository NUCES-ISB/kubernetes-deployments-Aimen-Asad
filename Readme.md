Flask & PostgreSQL Kubernetes Deployment

This repository contains a Kubernetes deployment for a Flask web application connected to a PostgreSQL database using Minikube.

Project Structure

k8s-flask-app/
│── manifests/
│   │── deployment/
│   │   │── flask-deployment.yaml
│   │   │── postgres-deployment.yaml
│   │── service/
│   │   │── flask-service.yaml
│   │   │── postgres-service.yaml
│   │── configmap/
│   │   │── postgres-configmap.yaml
│   │── secret/
│   │   │── postgres-secret.yaml
│── app/
│   │── Dockerfile
│   │── requirements.txt
│   │── app.py
│── README.md

Setup & Deployment Instructions

1️⃣ Start Minikube

Ensure Minikube is running:

minikube start

2️⃣ Build and Push Flask App Image

If using Docker Hub (Recommended):

docker build -t yourdockerhub/flask-app:v1 ./app
docker push yourdockerhub/flask-app:v1

If using Minikube’s local image:

docker build -t flask-app:v1 ./app
minikube image load flask-app:v1

3️⃣ Deploy PostgreSQL Configuration and Secrets

kubectl apply -f manifests/configmap/
kubectl apply -f manifests/secret/

4️⃣ Deploy PostgreSQL & Flask Applications

kubectl apply -f manifests/deployment/
kubectl apply -f manifests/service/

5️⃣ Verify Pods & Services

kubectl get pods
kubectl get services

6️⃣ Access the Flask Application

minikube service flask-service

This will open the Flask app in your default browser.

🔄 Scaling Flask Deployment

To increase the number of Flask replicas:

kubectl scale deployment flask-deployment --replicas=4

To decrease the number of Flask replicas:

kubectl scale deployment flask-deployment --replicas=2

Check pod status:

kubectl get pods

🛠 Debugging Tips

If any pod is stuck, describe it:

kubectl describe pod <pod-name>

Check logs for issues:

kubectl logs <pod-name>

