# GitOps Workflow Using ArgoCD on Kubernetes

## Objective
Implement GitOps to automate Kubernetes deployments by syncing with a GitHub repository using ArgoCD.

### Tools Used:
- **EC2 (Ubuntu)**: Cloud infrastructure host
- **K3s**: Lightweight Kubernetes distribution
- **ArgoCD**: GitOps deployment controller
- **GitHub**: Version control for manifests
- **Docker**: Building and pushing container image

## ⚙️ Setup Step
### Taking Ubuntu instance with t3.medium  
### Install K3s on EC2
### Setting kubectl for the current user 
### Installing ArgoCD 
### Accessing ArgoCD securely thru local from terminal
### kubectl edit svc argocd-server -n argocd → Changing the clusterIP to NodePort
### - Now we can access the ArgoCD UI thru local host → localhost:8080
- to get the ArgoCD password to login
![]()

### Creating deployment.yaml, service.yaml for my Nginx application, then
### configuring application.yaml files to sync my Git repository with my Kubernetes cluster 
### pushing them to my Github Repo
### then refreshing the ArgoCD 
### Updated replicas via git commits
### - kubectl get svc nginx-service → gives the port no. for nginx,
- enabling the port in security group of the instance and then accessing it





