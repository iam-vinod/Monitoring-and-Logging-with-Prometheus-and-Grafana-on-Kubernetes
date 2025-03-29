📌 Project Overview

This project sets up Prometheus and Grafana for monitoring a Kubernetes cluster using Minikube and Helm.

📂 Project Folder Structure

Monitoring-Logging-Prometheus-Grafana/
├── k8s/
│   ├── namespace.yaml
│   ├── prometheus-values.yaml
│   ├── grafana-dashboards/
│   │   ├── node-exporter-dashboard.json
│   │   ├── pod-monitoring-dashboard.json
├── .github/
│   ├── workflows/
│   │   ├── deploy.yml
├── README.md

✅ Prerequisites to Install

Install and configure Kubectl

Install Minikube

Install Helm

✅ Next Steps

🚀 Setup Instructions

Step 1: Start Minikube

minikube start --memory=4096 --cpus=2

Step 2: Create a Namespace for Monitoring

kubectl create namespace monitoring

Step 3: Install Prometheus & Grafana using Helm

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring

Step 4: Verify Running Services

kubectl get svc -n monitoring

Step 5: Access Grafana

kubectl port-forward svc/prometheus-grafana 3000:80 -n monitoring

Now, open Grafana in your browser:👉 http://localhost:3000

Step 6: Get Grafana Login Credentials

kubectl get secret --namespace monitoring prometheus-grafana -o jsonpath="{.data.admin-user}" | base64 --decode

kubectl get secret --namespace monitoring prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode

Use these credentials to log in to Grafana.

🎯 Why This Approach?

✔ No need for cloud infrastructure (AWS EKS, IAM, etc.)

✔ No need to configure Load Balancers or networking

✔ Fast deployment (~5 minutes)

✔ Everything runs locally

🔥 Next Steps

Add custom dashboards for monitoring specific applications.

Configure Alertmanager for setting up alerts.

Deploy to AWS EKS for production monitoring.



