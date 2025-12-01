# devops-assignment
Assignment for creating  a complete CI/CD infrastructure pipeline on AWS using Terraform, Kubernetes, ArgoCD.

This repository contains the code and configuration I used to build a complete CI/CD setup on AWS using Terraform, EKS, Kubernetes, and ArgoCD.

The setup provisions an EKS cluster, deploys an NGINX application, and uses ArgoCD for GitOps based continuous delivery.

This application is exposed through an Ingress controller with a DNS hostname(http://mydemonginx.nosky.io/).


1. Infrastructure – Terraform (EKS Cluster)

All Terraform files are under the terraform/ folder.

The Terraform setup does the following:

Creates a dedicated VPC

Deploys an EKS cluster 

Creates a managed node group

Outputs cluster endpoint and cluster name

Generates kubeconfig for connecting to the cluster

Commands used:

terraform init

terraform plan -out=tfplan

terraform apply tfplan

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

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode - Initial ArgoCD Password


<img width="1319" height="624" alt="image" src="https://github.com/user-attachments/assets/b0455fd6-5197-437b-bc6c-2e756590abe3" />

4. Accessing the NGINX Application

   I tested the application using: kubectl port-forward svc/nginx-service 9090:80
                                   http://localhost:9090

<img width="844" height="414" alt="image" src="https://github.com/user-attachments/assets/38712e05-921b-450e-b441-77a6edaf9b3e" />

5. Ingress + DNS

To expose NGINX publicly, I installed the ingress-nginx controller

Once the LoadBalancer IP was available, I configured an Ingress resource and used a DNS Domain.

<img width="1365" height="551" alt="image" src="https://github.com/user-attachments/assets/4ac9de6b-ba89-469b-9339-63f9c368deba" />














