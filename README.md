# 🛒 Best Buy Cloud-Native Microservices Application (AKS + MongoDB)

---

## 📌 Project Overview

This project is a **cloud-native microservices application** deployed on **Azure Kubernetes Service (AKS)**.
It simulates a Best Buy–style system where users can browse products, place orders, and admins can manage/view those orders.

The application follows a **microservices architecture** and uses **MongoDB for persistent storage**.

---

## 🏗️ Architecture Diagram

👉 *(Insert your Draw.io diagram image here — very important for marks)*

Example:

```text
[ User ]
   ↓
[ Store Front (NGINX + Vue) ]  --->  [ Product Service ]
           ↓
     [ Order Service ]  --->  [ MongoDB ]
           ↓
     [ Store Admin ]
```

---

## 🏗️ Architecture Components

* **Store Front** → Customer UI (Vue + NGINX)
* **Store Admin** → Admin UI (Vue + NGINX)
* **Product Service** → Provides product data
* **Order Service** → Handles order creation and retrieval
* **MongoDB** → Stores orders persistently

---

## 🔁 Application Flow

1. User opens Store Front → requests products from `product-service`
2. User places an order → request goes to `order-service`
3. `order-service` stores order in **MongoDB**
4. Admin UI fetches orders from `order-service`
5. Orders are retrieved from MongoDB

---

## 🧰 Technologies Used

* Docker 🐳
* Kubernetes (AKS) ☸️
* Node.js (Fastify)
* MongoDB 🍃
* NGINX
* Azure CLI
* GitHub

---

## 📂 Project Structure

```text
bestbuy-cloud-native-deployment/
│
├── namespace.yaml
├── mongodb-deployment.yaml
├── mongodb-service.yaml
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

| Service         | Docker Image                                     |
| --------------- | ------------------------------------------------ |
| Product Service | vijayxavierwalter/bestbuy-product-service:latest |
| Order Service   | vijayxavierwalter/bestbuy-order-service:latest   |
| Store Front     | vijayxavierwalter/bestbuy-store-front:latest     |
| Store Admin     | vijayxavierwalter/bestbuy-store-admin:latest     |

---

## 🔗 Links Table (Required)

| Component                    | Link                                                               |
| ---------------------------- | ------------------------------------------------------------------ |
| Store Front Repo             | *(add GitHub link)*                                                |
| Store Admin Repo             | *(add GitHub link)*                                                |
| Product Service Repo         | *(add GitHub link)*                                                |
| Order Service Repo           | *(add GitHub link)*                                                |
| Deployment Repo              | *(add GitHub link)*                                                |
| Docker Hub - Product Service | https://hub.docker.com/r/vijayxavierwalter/bestbuy-product-service |
| Docker Hub - Order Service   | https://hub.docker.com/r/vijayxavierwalter/bestbuy-order-service   |
| Docker Hub - Store Front     | https://hub.docker.com/r/vijayxavierwalter/bestbuy-store-front     |
| Docker Hub - Store Admin     | https://hub.docker.com/r/vijayxavierwalter/bestbuy-store-admin     |

---

## ☸️ AKS Deployment Instructions

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

### 4️⃣ Deploy Application

```bash
kubectl apply -f namespace.yaml
kubectl apply -f .
```

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

## 🗄️ MongoDB Integration

### Why MongoDB?

Initially, the application used **in-memory storage**, which caused data loss when containers restarted.

MongoDB was introduced to:

* Persist order data
* Enable scalability
* Follow cloud-native best practices

---

### MongoDB Connection

```text
mongodb://mongodb:27017
```

---

## 🧪 MongoDB Testing

### Persistence Test

1. Place order
2. Restart service:

```bash
kubectl rollout restart deployment order-service -n bestbuy
```

3. Refresh admin

👉 Order remains → MongoDB working

---

### Direct DB Query

```bash
kubectl exec -it deploy/mongodb -n bestbuy -- mongosh
```

```js
use bestbuy
db.orders.find().pretty()
```

---

## 🔧 Key Issues & Fixes

| Issue                 | Fix                 |
| --------------------- | ------------------- |
| NGINX config error    | Fixed `server {}`   |
| Service communication | Used Kubernetes DNS |
| Fastify binding       | Set `0.0.0.0`       |
| MongoDB error         | Fixed `crypto`      |
| Data loss             | Added MongoDB       |

---

## 🎥 Demo Video

👉 *(Add YouTube link here)*

---

## 👨‍💻 Author

**Vijay**

---

## 📢 Conclusion

This project demonstrates:

* Microservices architecture
* Docker containerization
* Kubernetes orchestration (AKS)
* Persistent storage using MongoDB
* End-to-end cloud deployment

---
