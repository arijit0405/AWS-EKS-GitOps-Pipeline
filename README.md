# devops-assignment
Assignment for creating  a complete CI/CD infrastructure pipeline on AWS using Terraform, Kubernetes, ArgoCD.

This repository contains the code and configuration I used to build a complete CI/CD setup on AWS using Terraform, EKS, Kubernetes, and ArgoCD.

The setup provisions an EKS cluster, deploys an NGINX application, and uses ArgoCD for GitOps based continuous delivery.

This application is exposed through an Ingress controller with a DNS hostname(http://mydemonginx.nosky.io/).


1. Infrastructure – Terraform (EKS Cluster)

All Terraform files are under the terraform/ folder.

The Terraform setup does the following:

Creates a dedicated VPC

Deploys an EKS cluster (1.30)

Creates a managed node group

Outputs cluster endpoint and cluster name

Generates kubeconfig for connecting to the cluster

<img width="1165" height="621" alt="image" src="https://github.com/user-attachments/assets/7b17fe2d-aa2f-44d6-a793-9d732d5629e6" />

2. Application Deployment – Kubernetes Manifests

   Inside the manifests/ folder are:

deployment.yaml — NGINX Deployment (2 replicas)

service.yaml — ClusterIP service exposing the app

ingress.yaml — Ingress for external access 

The manifests were applied automatically using ArgoCD.


3. GitOps with ArgoCD

ArgoCD was installed in the cluster inside the argocd namespace.

The ArgoCD Application definition is inside argocd/application.yaml.

This Application watches the repository and deploys anything inside the manifests/ folder automatically.

ArgoCD UI Access

I accessed the ArgoCD UI using port-forwarding

Then visited: https://localhost:9091

<img width="1319" height="624" alt="image" src="https://github.com/user-attachments/assets/b0455fd6-5197-437b-bc6c-2e756590abe3" />











