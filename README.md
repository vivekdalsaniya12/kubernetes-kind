
# 🚀 Kubernetes NGINX Setup (Local KIND Cluster)

This project demonstrates a basic Kubernetes setup using **`kind` (Kubernetes IN Docker)** on a local machine. It includes:

- ✅ A standalone NGINX Pod
- ✅ A Deployment with 3 NGINX replicas
- ✅ A NodePort Service exposing NGINX on port `30001`

---

## 📦 Step 1: Clone This Repo

```bash
git clone https://github.com/vivekdalsaniya12/kubernetes-kind.git
cd kubernetes-kind
```

---

## 🧰 Step 2: Install Prerequisites

### 🔹 Install `kubectl`

```bash
sudo apt update
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

### 🔹 Install `kind`

```bash
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

---

## 🧱 Step 3: KIND Cluster Commands

### ✅ Create Cluster

```bash
kind create cluster --name my-cluster --config cluster.yml
```

### 🔍 Check Cluster

```bash
kubectl cluster-info --context kind-my-cluster
```

### 📋 List Clusters

```bash
kind get clusters
```

### ❌ Delete Cluster

```bash
kind delete cluster --name my-cluster
```

---

## 📁 Step 4: Kubernetes Manifests in This Repo

- `nginx-deployment.yaml` – Deployment with 3 replicas
- `nginx-service.yaml` – NodePort service on port `30001`

---

## ⚙️ Step 5: Apply Resources

```bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
```

---

## 🔎 Step 6: Verify Resources

```bash
kubectl get nodes
kubectl get pods -o wide
kubectl get svc
```

Optional detailed checks:

```bash
kubectl describe deployment nginx-deployment
kubectl describe service nginx-service
```

---

## 🌐 Step 7: Access NGINX Locally

Since `kind` runs in Docker, use the Docker host IP to access NGINX:

```bash
curl http://localhost:30001
```

Or open in browser:

```
http://localhost:30001
```

---

## 🧼 Step 8: Cleanup

```bash
kubectl delete -f nginx-deployment.yaml
kubectl delete -f nginx-service.yaml
```

Or delete everything:

```bash
kubectl delete -f .
```

---

## 📘 References

- [KIND Documentation](https://kind.sigs.k8s.io/)
- [Kubernetes Official Docs](https://kubernetes.io/docs/)

