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
```
 curl -sfL https://get.k3s.io | sh -
```
### Setting kubectl for the current user 
```
mkdir -p $HOME/.kube
sudo cp /etc/rancher/k3s/k3s.yaml $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
### Installing ArgoCD
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Accessing ArgoCD securely thru local from terminal
```
nohup kubectl port-forward svc/argocd-server -n argocd 8080:8083 > portforward.log 2>&1 &
ssh -i "YourKey.pem" -L 8080:localhost:8080 ubuntu@your-remote-ip
```


### Checking the nodes - kubectl get nodes
![](https://github.com/deepakbehera11/GitOps-Workflow-using-ArgoCD-on-Kubernetes/blob/eb7173ee65c3a7b59d567875a39ccd6a72e27060/assests/Screenshot-01.png)

### kubectl edit svc argocd-server -n argocd → Changing the clusterIP to NodePort
### - Now we can access the ArgoCD UI thru local host → localhost:8080 
### to get the ArgoCD password to login
```
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```

### Creating deployment.yaml, service.yaml for my Nginx application, then
### configuring application.yaml files to sync my Git repository with my Kubernetes cluster 
### pushing them to my Github Repo
### then refreshing the ArgoCD 
![](https://github.com/deepakbehera11/GitOps-Workflow-using-ArgoCD-on-Kubernetes/blob/f98ad7c913b54b58298e8260a922b2f8e976bed2/assests/Screenshot-02.png)
![](https://github.com/deepakbehera11/GitOps-Workflow-using-ArgoCD-on-Kubernetes/blob/f98ad7c913b54b58298e8260a922b2f8e976bed2/assests/Screenshot-03.png)

### Updated replicas via git commits
![](https://github.com/deepakbehera11/GitOps-Workflow-using-ArgoCD-on-Kubernetes/blob/f98ad7c913b54b58298e8260a922b2f8e976bed2/assests/Screenshot-04.png)

### - kubectl get svc nginx-service → gives the port no. for nginx,
### enabling the port in security group of the instance and then accessing my nginx





