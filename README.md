# 🚀 Kubernetes Cluster Deployment on AWS 

## 📌 Architecture Overview
This project deploys a Kubernetes-based application with a well-structured architecture. The key components include:

- 🌐 **Application Load Balancer**: Distributes incoming traffic.
- 🔀 **Ingress Controller**: Manages access to the Kubernetes services.
- 🏗️ **Tomcat Service**: Handles web requests.
- 🛠️ **Microservices**:
  - 📩 **RMQService** (RabbitMQ for messaging)
  - 🗄️ **MCService** (Memcache for caching)
  - 🛢️ **DBService** (Database service)
- 💾 **Persistent Storage**:
  - 🏠 **DB Pod**: Stores database data.
  - 📜 **PersistentVolumeClaim (PVC)**: Requests storage.
  - 📦 **StorageClass**: Manages storage provisioning.
  - ☁️ **Amazon EBS**: Cloud storage backend.
- 🔑 **Secrets Management**: Secure credentials storage.

![Architecture Diagram](https://github.com/abdoelwaly/aws-kubernetes-learning-project/blob/main/architecture/project-architecture.jpg)

## 📖 Deployment Instructions
Follow these steps to deploy the project on AWS Kubernetes:

### 1️⃣ Clone the Repository
```sh
 git clone https://github.com/abdoelwaly/aws-kubernetes-learning-project.git
```

### 2️⃣ Setup Ingress
Create the ingress controller, which will provision an AWS Load Balancer:
```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/aws/deploy.yaml
```
✅ Verify the installation:
```sh
kubectl get ns 
kubectl get pods --namespace ingress-nginx
```

### 3️⃣ Change Directory to Kubernetes Definitions
```sh
cd kube-definition
```

### 4️⃣ Create Persistent Volume in AWS
```sh
kubectl create -f dbpvc.yaml
```

### 5️⃣ Deploy All Services
```sh
kubectl create -f .
```

### 6️⃣ Verify Deployments
Check the status of pods, deployments, and services:
```sh
kubectl get pods, deploy, svc
```
📌 For more details:
```sh
kubectl describe pod <pod-name>
```
🗑️ To delete a deployment:
```sh
kubectl delete -f file.yaml
```

### 7️⃣ Retrieve Pod IP
```sh
kubectl describe pod kuprjapp
```

### 8️⃣ Validate Service Endpoint
Ensure the endpoint IP matches the pod:
```sh
kubectl describe svc kuprjapp-service
```

### 9️⃣ Verify Storage Class
```sh
kubectl get sc
```

### 🔟 Validate Ingress
```sh
kubectl get ingress
kubectl describe ingress kuprjapp
```
Ensure the backend service is set to `kuprjapp-service:8080` with the correct IP.

### 🏁 Create a DNS Record
Point your DNS provider's record to the Ingress endpoint for proper routing.

## 🎯 Conclusion
Following these steps will successfully deploy your Kubernetes-based application on AWS, leveraging best practices for scalability, persistence, and service discovery. 🚀

