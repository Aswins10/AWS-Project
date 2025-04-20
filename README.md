# ☁️ AWS EKS - Amazon Elastic Kubernetes Service

A comprehensive guide to understanding, setting up, and deploying containerized applications using **Amazon Elastic Kubernetes Service (EKS)**. This project is designed for learners, engineers, and DevOps professionals aiming to manage Kubernetes at scale with the power of AWS.

---

## 📖 Table of Contents

1. [📘 Introduction](#introduction)  
2. [🔧 Kubernetes Fundamentals](#kubernetes-fundamentals)  
   - EKS vs. Self-Managed Kubernetes  
3. [☁️ Setting Up AWS for EKS](#setting-up-aws-for-eks)  
   - Creating AWS Account & IAM Users  
   - Configuring AWS CLI & kubectl  
   - Networking & Security Group Configuration  
4. [🚀 Launching Your First EKS Cluster](#launching-your-first-eks-cluster)  
   - Using AWS Console  
   - Using AWS CLI  
   - Authentication & Cluster Access  
5. [📦 Deploying Applications on EKS](#deploying-applications-on-eks)  
   - Dockerizing Applications  
   - Writing Kubernetes YAMLs  
   - Step-by-step Deployment

---

## 📘 Introduction

Amazon EKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications using Kubernetes on AWS. This guide explores the essentials from setup to real-world deployment strategies.

---

## 🔧 Kubernetes Fundamentals

### 🆚 EKS vs. Self-Managed Kubernetes

**EKS (Managed)**  
✅ Automatic updates, high availability, AWS integrations, monitoring with CloudWatch, and security compliance  
❌ Higher cost, limited flexibility on low-level Kubernetes configurations  

**Self-Managed (on EC2)**  
✅ Full control, cost-effective (Spot/Reserved Instances), early feature access  
❌ Complex to manage, requires manual upgrades, scaling, and security setup  

---

## ☁️ Setting Up AWS for EKS

### ✅ Creating AWS Account & IAM Users

- Create an [AWS Account](https://aws.amazon.com/)  
- Setup IAM users with programmatic and console access  
- Configure MFA for security  
- Grant roles with EKS-related permissions

### ⚙️ Configuring AWS CLI and `kubectl`

- Install [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
- Run `aws configure` to set credentials
- Install [kubectl](https://kubernetes.io/docs/tasks/tools/)
- Configure `kubectl` using:
  ```bash
  aws eks update-kubeconfig --name your-cluster-name
  ```

### 🔐 Preparing Networking and Security

- **VPC Setup:** Create VPC, subnets, route tables  
- **Security Groups:** Allow SSH (22), Kubernetes (6443), and ingress/egress for nodes  
- **Internet Gateway (IGW):** Attach IGW for outbound internet access  
- **IAM Roles & Policies:** Create EKS-specific IAM roles for node groups with policies for EC2, ECR, ELB, etc.

---

## 🚀 Launching Your First EKS Cluster

### 1. Using AWS Console

- Go to **EKS > Create Cluster**
- Configure control plane and node groups
- Use default or custom VPC and subnets

### 2. Using AWS CLI

```bash
eksctl create cluster --name demo-cluster --region us-west-2 --nodes 2
```

### 3. Authenticating with the EKS Cluster

- Verify connection:
  ```bash
  kubectl get svc
  ```

---

## 📦 Deploying Applications on EKS

### 🐳 Containerize Your App with Docker

- Create Dockerfile  
- Build and push to [Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)

### 📝 Write Kubernetes YAML Files

- Define **Deployment**, **Service**, and optionally **Ingress** for routing

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: app
        image: <your-ecr-image-url>
        ports:
        - containerPort: 80
```

### 📥 Deploy to EKS

```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

---

## 🙋‍♂️ Author

**Aswin S Krishna**  
B.Tech in Computer Science & Engineering  
Lovely Professional University
