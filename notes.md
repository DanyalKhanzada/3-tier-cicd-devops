----------------------------------------All Nodes--------------------------------------------------

sudo-apt-get update

sudo apt install docker.io -y

sudo chmod 666 /var/run/docker.sock

sudo apt-get install -y apt-transport-https ca-certificates curl gnupg

sudo mkdir -p -m 755 /etc/apt/keyrings

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update

sudo apt install -y kubeadm=1.30.0-1.1 kubelet=1.30.0-1.1 kubectl=1.30.0-1.1

* change permission of VI - sudo chmod +x 1.sh


----------------------------------MasterNode-------------------------------------------------------

sudo kubeadm init --pod-network-cidr=10.244.0.0/16

# The output of above command to run in worker nodes

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u) :$(id -g) $HOME/.kube/config

kubectl apply -f
https://raw.githubusercontent.com/projectcalico/calico/v3.24.0/manifests/calico.yaml

kubectl apply -f
https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml


---------------------------------------Steps-------------------------------------------------------

1. # How to connect clusters?
- run command : sudo kubeadm init --pod-network-cidr=10.244.0.0/16
- use the token to connect the master with worker 

2. # Create kube directory which will have Kube config file for authentication

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u) :$(id -g) $HOME/.kube/config

3. # kubectl - Calico project for networking and nginx
kubectl apply -f
https://raw.githubusercontent.com/projectcalico/calico/v3.24.0/manifests/calico.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml




