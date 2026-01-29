# Launch-Kubernetes----aws-cli-kubectl-minikube

Hands-on Kubernetes setup and local deployment using Minikube on Windows.
This project uses Minikube to run a local Kubernetes cluster on Windows 11.

## Kubernetes Resources Created

The following Kubernetes objects were created and verified in the Minikube cluster:

Deployments

ReplicaSets

Pods

### Create an EC2 instance

<!-- if u are using window skip this -->

- Dependencies required

Python3
AWS CLI
kubectl

- Follow below step :

- Install dependencies
- Python3  
  sudo apt update  
  sudo apt install -y python3 python3-pip

Verify  
python3 --version  
pip3 --version

- AWS CLI (Ubuntu 24.04 compatible)  
  sudo snap install aws-cli --classic

Verify  
aws --version

- kubectl
- Add Kubernetes repository  
  sudo apt-get update  
  sudo apt-get install -y ca-certificates curl apt-transport-https

sudo mkdir -p /etc/apt/keyrings  
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | \
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | \
sudo tee /etc/apt/sources.list.d/kubernetes.list

- Install kubectl  
  sudo apt-get update  
  sudo apt-get install -y kubectl

Verify  
kubectl version --client

- Final check  
  python3 --version  
  aws --version  
  kubectl version --client

- Install KOPS  
  curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

chmod +x kops-linux-amd64

sudo mv kops-linux-amd64 /usr/local/bin/kops

### Download Minikube directly to C:\minikube

mkdir -p /c/minikube
curl -Lo /c/minikube/minikube.exe https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe

- start your docker engin

<!-- Start minikube in docker driver -->

minikube start --driver=docker

- Now do  
  kunectl get nodes

u will notice kubectl is already connected to your k8s cluster

###directly creating pods

- run the yaml file to create pod with below commands  
  kubectl create -f pod.yaml

- now u can view your container running with command  
  kubectl get pods -o wide

--to see your application running

<!-- do -->

minikube ssh

<!-- inside docker@minikube -->

curl {ip address u get form "kubectl get pods -o wide" }

<!-- u will see ur application running -->

###creating deployment
kubectl apply -f deployment.yaml

<!-- You can see deployment, replicaset and pods being created just through deployment -->

kubectl get deploy

###lets observe auto healing

<!-- to observe pods live, open new terminal and type -->

kubectl get pods -w

<!-- then delete one pods in another terminal -->

kubectl delete pod nginx-deployment-77bc6bd484-6zlkh

<!-- you can see even before termination of pods is done, new container is being created -->
<!-- its replica set purpose to maintain to maintain a stable set of replica pods at
any given time and its doing same -->

<!-- to delete deployment -->

kubectl delete deployment nginx-deployment

- Refrence page for help with commands  
  https://kubernetes.io/pt-br/docs/reference/kubectl/cheatsheet/
