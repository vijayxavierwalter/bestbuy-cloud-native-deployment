# 🛒 Best Buy Cloud-Native Microservices Application

## 📌 Project Overview

This project is a **cloud-native microservices application** deployed on **Azure Kubernetes Service (AKS)**.
It simulates a simplified Best Buy system with product browsing, order placement, and admin management.

---

## 🏗️ Architecture

The application is built using a **microservices architecture**:

* **Store Front (Frontend)** → Customer UI
* **Store Admin (Frontend)** → Admin UI
* **Product Service (Backend)** → Handles product data
* **Order Service (Backend)** → Handles orders

### 🔁 Flow

1. User browses products → `product-service`
2. User places order → `order-service`
3. Admin views orders → `order-service`

---

## 🧰 Technologies Used

* Docker 🐳
* Kubernetes (AKS) ☸️
* Node.js (Fastify)
* NGINX
* Azure CLI
* GitHub

---

## 📂 Project Structure

```
bestbuy-cloud-native-deployment/
│
├── namespace.yaml
├── product-service-deployment.yaml
├── product-service-service.yaml
├── order-service-deployment.yaml
├── order-service-service.yaml
├── store-front-deployment.yaml
├── store-front-service.yaml
├── store-admin-deployment.yaml
├── store-admin-service.yaml
```

---

## 🐳 Docker Images

| Service         | Docker Image                                       |
| --------------- | -------------------------------------------------- |
| Product Service | `vijayxavierwalter/bestbuy-product-service:latest` |
| Order Service   | `vijayxavierwalter/bestbuy-order-service:latest`   |
| Store Front     | `vijayxavierwalter/bestbuy-store-front:latest`     |
| Store Admin     | `vijayxavierwalter/bestbuy-store-admin:latest`     |

---

## ☸️ Kubernetes Deployment (AKS)

### 1️⃣ Create Resource Group

```bash
az group create --name rg-bestbuy-aks --location canadacentral
```

### 2️⃣ Create AKS Cluster

```bash
az aks create \
  --resource-group rg-bestbuy-aks \
  --name bestbuy-aks-cluster \
  --node-count 1 \
  --generate-ssh-keys
```

### 3️⃣ Connect to AKS

```bash
az aks get-credentials \
  --resource-group rg-bestbuy-aks \
  --name bestbuy-aks-cluster
```

---

### 4️⃣ Deploy to Kubernetes

```bash
kubectl apply -f namespace.yaml
kubectl apply -f .
```

---

### 5️⃣ Verify Deployment

```bash
kubectl get pods -n bestbuy
kubectl get svc -n bestbuy
```

---

## 🌐 Application URLs

| Service     | URL                 |
| ----------- | ------------------- |
| Store Front | http://4.172.68.214 |
| Store Admin | http://4.172.67.89  |

---

## ✅ Features Implemented

* Browse products
* Add items to cart
* Place orders
* View orders in admin dashboard
* Microservices communication via Kubernetes
* Containerized using Docker
* Deployed to AKS

---

## 🔧 Key Fixes & Learnings

* Fixed **NGINX config issue** (`location directive not allowed`)
* Fixed **service communication issue** using Kubernetes service names
* Fixed **Fastify binding issue** by using:

  ```
  -a 0.0.0.0
  ```
* Ensured all services run inside same Kubernetes namespace

---

## 🎥 Demo Video

👉 *(Add your YouTube link here)*

---

## 📎 GitHub Repositories

* Store Front: *(add link)*
* Store Admin: *(add link)*
* Product Service: *(add link)*
* Order Service: *(add link)*
* Deployment Repo: *(add link)*

---

## 👨‍💻 Author

**Vijay**

---

## 📢 Conclusion

This project demonstrates:

* Microservices architecture
* Containerization with Docker
* Orchestration using Kubernetes
* Cloud deployment using Azure AKS

---
