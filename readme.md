# Kubernetes Nginx Deployment (Minikube)

This project deploys an Nginx web server to a local Kubernetes cluster using Minikube.  
It creates a Deployment running `nginx:latest` and exposes it using a NodePort Service on port `30001`.

---

## 📋 Prerequisites

Make sure the following are installed:

- Docker
- kubectl
- Minikube

Verify installations:

```bash
docker --version
kubectl version --client
minikube version
```

---

# 🚀 Run the Project (Start to Finish)

Follow these steps exactly.

---

## 1️⃣ Start Minikube

Start your local Kubernetes cluster:

```bash
minikube start
```

Verify the cluster is running:

```bash
kubectl get nodes
```

Expected output:

```
minikube   Ready
```

---

## 2️⃣ Deploy Nginx

Make sure you are in the directory containing:

```
nginx.yml
```

Then deploy:

```bash
kubectl apply -f nginx.yml
```

Verify the resources:

```bash
kubectl get pods
kubectl get svc
```

You should see:
- A pod with STATUS `Running`
- A service named `nginx-service`
- `80:30001/TCP` listed under PORT(S)

---

# 🌐 Access the Webpage

## ✅ Recommended Method

```bash
minikube service nginx-service
```

This automatically opens your browser to the Nginx welcome page.

---

## ✅ Manual Method

Get the Minikube IP:

```bash
minikube ip
```

Then open your browser and go to:

```
http://<minikube-ip>:30001
```

Example:

```
http://192.168.49.2:30001
```

You should see:

```
Welcome to nginx!
```

---

# 🧹 Shut Everything Down

## Delete the Deployment and Service

```bash
kubectl delete -f nginx.yml
```

Verify deletion:

```bash
kubectl get pods
kubectl get svc
```

---

## Stop Minikube

```bash
minikube stop
```

---

## (Optional) Completely Reset Minikube

This deletes the entire cluster:

```bash
minikube delete
```

---

# 🔄 Quick Restart Workflow

Start everything again:

```bash
minikube start
kubectl apply -f nginx.yml
minikube service nginx-service
```

Stop everything:

```bash
kubectl delete -f nginx.yml
minikube stop
```

---

# 📁 Project Structure

```
.
├── nginx.yml
└── README.md
```

---

# 🧠 How It Works

- The **Deployment** creates a Pod running Nginx.
- The **NodePort Service** exposes the Pod externally on port `30001`.
- Minikube runs a local Kubernetes cluster for development and testing.

---

You are now running Nginx inside a real Kubernetes cluster locally 🚀