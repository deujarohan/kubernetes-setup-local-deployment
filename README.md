# Launch-Kubernetes----aws-cli-kubectl-minikube

## Kubernetes Installation Using KOPS on EC2

### Create an EC2 instance

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

- Now do  
  kunectl get nodes

u will notice kubectl is already connected to your k8s cluster

- run the yaml file to create pod with below commands  
  kubectl create -f pod.yaml

- now u can view your container running with command  
  kubectl get pods -o wide

- Refrence page for help with commands  
  https://kubernetes.io/pt-br/docs/reference/kubectl/cheatsheet/
