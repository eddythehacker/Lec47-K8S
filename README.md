# Lec47-K8S
K8S Control Plaine Setup
Set by Step

Step1: (On Master & worker node)

sudo su
cd
hostname master(in master, in node use node1)
exec bash(in master, in node also)
apt-get update  
apt-get install docker.io -y
systemctl restart docker
systemctl enable docker  
sudo apt-get install -y apt-transport-https ca-certificates curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -  
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
apt-get update
apt install kubeadm kubectl kubelet kubernetes-cni -y  

Step2: (On Master)

   kubeadm init --pod-network-cidr=192.168.0.0/16 (just use kubeadm init)
   Copy the token and paste it into the worker node.

Step3:(On Master)

    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml


now check the nodes are connected or not with this command

      kubectl get nodes
     o/p ---> master - ready
              node1  - ready 

Our Kubernetes installation and configuration are complete
