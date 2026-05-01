![Terraform](https://img.shields.io/badge/IaC-Terraform-blue)
![AWS](https://img.shields.io/badge/Cloud-AWS-orange)
![Kubernetes](https://img.shields.io/badge/Orchestration-Kubernetes-blue)

---

# AWS EKS Cluster with Terraform

This project provisions a highly available Amazon EKS cluster on AWS using Terraform, including networking, managed node groups, and Kubernetes add-ons.

---

## 🚀 Overview

This infrastructure deploys:

- A custom VPC with public and private subnets
- A managed Amazon EKS cluster
- EKS managed node groups
- Core Kubernetes add-ons (CoreDNS, kube-proxy, VPC CNI)
- NAT Gateway for private subnet internet access

The setup follows Infrastructure as Code (IaC) best practices using Terraform modules.

---

## ## 🎯 Purpose

This project demonstrates hands-on experience with:
- Infrastructure as Code using Terraform
- AWS networking and EKS cluster provisioning
- Kubernetes-based application infrastructure
- Designing scalable and secure cloud environments

---

## 🏗️ Architecture

- **Region:** eu-west-2 (London)
- **VPC:** Custom VPC with DNS support
- **Subnets:**
  - Public subnets (for load balancers)
  - Private subnets (for worker nodes)
- **EKS Cluster:**
  - Kubernetes version: 1.33
  - Public API endpoint enabled
- **Node Group:**
  - Instance type: t2.small
  - Auto scaling: min (1), max (3), desired (3)

---

## 📦 Modules Used

- terraform-aws-modules/vpc/aws
- terraform-aws-modules/eks/aws

---

## ⚙️ Features

- Fully automated infrastructure provisioning
- Managed Kubernetes control plane (EKS)
- Scalable worker nodes using managed node groups
- Secure networking with private subnets
- NAT Gateway for outbound internet access
- Kubernetes-ready subnet tagging for load balancers
- Core add-ons installed:
  - CoreDNS
  - kube-proxy
  - VPC CNI
  - EKS Pod Identity Agent

---

## 🛠️ Prerequisites

Before you begin, ensure you have:

- Terraform installed (>= 1.0)
- AWS CLI configured (`aws configure`)
- IAM permissions to create:
  - VPC
  - EKS cluster
  - EC2 instances
  - IAM roles

---

## 📄 Variables

Define the following variables (e.g. in `terraform.tfvars`):

```hcl
vpc_cidr_block            = "10.0.0.0/16"
private_subnet_cidr_block = ["10.0.1.0/24", "10.0.2.0/24"]
public_subnet_cidr_block  = ["10.0.101.0/24", "10.0.102.0/24"]
```

---

## 📁 Project Structure

.
├── eks-cluster.tf
├── vpc.tf
├── provider.tf
├── variables.tf
├── terraform.tfvars
└── README.md

---

## ▶️ Usage

### 1. Initialize Terraform

```bash
terraform init
```

### 2. Plan the deployment

```bash
terraform plan
```

### 3. Apply the configuration

```bash
terraform apply
```

---
## 🔐 Accessing the cluster

After deployment, configure kubectl:
```bash
aws eks update-kubeconfig --region eu-west-2 --name myapp-eks-cluster
```

Verify:
```bash
kubectl get nodes
```

---
## 🧹 Cleanup

To destroy all resources:
```bash
terraform destroy
```

---
## 📌 Notes

- Public endpoint access is enabled for simplicity (not recommended for production)
- Uses a single NAT Gateway to reduce cost
- Designed for development/testing environments

---

## 📈 Future Improvements

- Add private API endpoint for EKS
- Implement Terraform remote state (S3 + DynamoDB)
- Add monitoring (Prometheus/Grafana)
- Integrate CI/CD pipeline for automated deployments
- Use more cost-efficient instance types (e.g., t3.small)

---

## 👤 Author

Olu Ayeni

DevOps & Cloud Engineer
