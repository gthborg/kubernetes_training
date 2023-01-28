# kubernetes master and worker nodes install and configuration steps


Run on Master worker nodes 
sudo hostnamectl set-hostname "k8s-master"
sudo exec bash

Run on Master worker nodes
sudo hostnamectl set-hostname "k8s-worker-01"
sudo exec bash

Run on Master and worker nodes
sudo apt-get update && apt-get install apt-transport-https ca-certificates curl software-properties-common gnupg2 -y
  
Run on Master and worker nodes
### Add Docker’s official GPG key
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

Run on Master and worker nodes
### Add Docker apt repository.
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

Run on Master and worker nodes
## Install Docker CE.
sudo apt-get update && apt-get install containerd.io docker-ce docker-ce-cli -y

Run on Master and worker nodes
sudo mkdir -p /etc/systemd/system/docker.service.d

Run on Master and worker nodes
# Restart docker.
sudo systemctl daemon-reload
sudo systemctl restart docker

Run on Master and worker nodes
sudo apt-get install apt-transport-https curl -y

Run on Master and worker nodes
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add

Run on Master and worker nodes
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"

Run on Master and worker nodes
sudo apt install  kubelet kubeadm kubectl -y

Run on Master 
sudo kubeadm version

Run on Master
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab

Run on Master
sudo kubeadm init --pod-network-cidr=10.244.0.0/16


mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config



execute these commands if master and workers are not able start/join to the cluster
rm /etc/containerd/config.toml
systemctl restart containerd


On worker nodes
kubeadm join 192.168.1.3:6443 --token m0dr9x.qz1njp8f6chdwa2r --discovery-token-ca-cert-hash sha256:6d49b7c2129c4c1a4a5bd2bcc03900d05c6a15ec5049fd37252286ca5e4c7aca


sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
