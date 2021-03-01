## Deploy Kubbernets Cluster on Your Own Laptop or Desktop

This Section of the Course teaches you to deploy a multi node Kubbernets Cluster on your Own Laptop or Desktop
Here we'll deploy a 3 Node Cluster, one Master Node and 2 Worker Nodes

### Create A Virtual Machines using VirtualBox

```
The VM size can be according to the Hardware Resources available on your Laptop/Desktop

### For Laptop/Desktop with 8 GB RAM

Master Node Size : - VM Size , 2 vCPU, 2 GB RAM
Worker Node Size : -  VM Size 2 vCPU , 2 GB RAM

### For Laptop/Deksktop with 16GB RAM

Master Node Size : - VM Size , 2 vCPU, 4 GB RAM
Worker Node Size : -  VM Size 2 vCPU , 4 GB RAM
```

### Install Ubuntu Server on One VM and setup static IP for each VM as follows.
```
First Disable the swap space ,because swap is not supported for Kubernates cluster nodes

$ sudo swapoff -a 

Network Settings for the VMs - Static IP
hostname: k8s-master.local
IP Address : 192.168.1.101

Install docker on the VM

$ curl -sSL https://get.docker.com | bash
$ sudo usermod -aG docker $USER
$ sudo systemctl enable docker

```
### Next Install kubeadm,kubectl,kubelet

You will install these packages on all of your machines:

kubeadm: the command to bootstrap the cluster.

kubelet: the component that runs on all of the machines in your cluster and does things like starting pods and containers.

kubectl: the command line util to talk to your cluster.

```
sudo apt update && sudo apt install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

After installing these packages stop the VM to be cloned.
```
### Clone the VM into 2 more VMs and name them as k8s-worker-1 and k8s-worker-2
```
VM2 :
hostname: k8s-worker-1 
IP Adresss : 192.168.1.102

VM3:
hostname: k8s-worker-2
Ip Address: 192.168.1.103

```
### Intialize the Kubernetes Master Node

```
$ sudo kubeadm init --apiserver-advertise-address=192.168.1.101 --pod-network-cidr=10.0.0.0/16

And wait for sometime ,nearly 5 mins, for all the components to be installed and intialized.

This command will result in output like this.......

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

After the command finishes, copy the join command to be used for setting up your worker nodes and joining them to the cluster.It ll be something like the following.

Change the docker cgroup driver to systemd.

Change the current detected "cgroupfs"  Docker cgroup driver. The recommended driver is "systemd"

$ sudo vi /lib/systemd/system/docker.service

add the following to the end of the line as follows

--exec-opt native.cgroupdriver=systemd

ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --exec-opt native.cgroupdriver=systemd

$ sudo systemctl daemon-reload
$ sudo systemctl restart docker

kubeadm join 192.168.1.101:6443 --token xxxxxxxxxxxxxxxxxx \
    --discovery-token-ca-cert-hash sha256:223f804xxxxx94fa061b40a08xxxxx257fc9a99xxxx888f7axxxxeddf5a75df
    
Now run this command on each of the worker nodes using root privilege.

$ sudo kubeadm join 192.168.1.101:6443 --token xxxxxxxxxxxxxxxxxx \
    --discovery-token-ca-cert-hash sha256:223f804xxxxx94fa061b40a08xxxxx257fc9a99xxxx888f7axxxxeddf5a75df
    
It ll output with the following details....
.........
This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.

```
