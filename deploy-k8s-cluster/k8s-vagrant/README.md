## Deploy Kubernates Clouster on your laptop using vagrant

# Clone this repo to your home directory

You can either choose the private networking or public networking between the kubernetes Hos VMs.

If you want to choose private networking then the vagrant file will create/choose the hostonly network from your VirtualBox networks.
If you choose to run the cluster in your home LAN network.

Edit the Vagrantfile based on your LAN network IP, if you are in your home network, most likely it ll be either 192.168.1.0 or 192.168.0.0, so edit the following based on your network and number of nodes required.Choose the Kubernates Master VM IPS address and change the network IP address too.

```
cd /kubernetes-dev/k8s-vagrant/

vi Vagrantfile

MASTER_COUNT = 1
NODE_COUNT   = 2
MASTER_IP    = "192.168.1.10"
MASTER_PORT  = "8443"
NODE_IP_NW   = "192.168.1."

$ vagrant up

```
It ll ask which the following, I am creating the VMs with a public network,instaed of private network, so that I can connect a LaodBalancer to my kubernetes Cluster

"master: Which interface should the network bridge to?" This question will be repeated for all your nodes.

Select which interface is connected to your home router for internet connection.

After successfully creting the cluster login to the Master node and test the kubernetes clusrer functionality by excuting the following.

```
$ vagrant ssh master

mkdir -p $HOME/.kube
sudo cp -Rf /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl cluster-info
kubectl get nodes

It should appear as the following

vagrant@master:~$ kubectl get nodes
NAME     STATUS   ROLES                  AGE     VERSION
master   Ready    control-plane,master   11m     v1.21.0
node1    Ready    <none>                 8m18s   v1.21.0
node2    Ready    <none>                 117s    v1.21.0

```

open the ~/.kube/config file and copy the contents of the file.
  
In another terminal, Create a config file in your laptop in the .kube dirctory present in the home directoty, for me it is /Users/pnayak/.kube

create and open the file /Users/pnayak/.kube/config with your favorite text editor, I used vi editor

$vi /Users/pnayak/.kube/config

copy the contents to the local configfile /Users/pnayak/.kube/config

Exit the Master node check the cluster from the laptop terminal

```

MacBook-Pro:k8s pnayak$ pwd
/Users/pnayak/k8s
MacBook-Pro:k8s pnayak$ kubectl get nodes
NAME     STATUS   ROLES                  AGE    VERSION
master   Ready    control-plane,master   15m    v1.21.0
node1    Ready    <none>                 12m    v1.21.0
node2    Ready    <none>                 6m5s   v1.21.0
MacBook-Pro:k8s pnayak$ 

If you want to installl the default kubernetes dashboard excuting the following

$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.2.0/aio/deploy/recommended.yaml

Access dashboard using proxy

$kubectl proxy
```

Access ui using
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

Get the token by the following command

$ kubectl -n kube-system describe secret default
  
# Install Opensource Dashboard named Octant
  
On your macbook you can use 
  
#brew install octant
After successfully install octant just run it with 
  
$octant
  
This will automatically take the kubernetes config file located at ~/.kube/config and open the browser with the kubaernetes cluster dashboard

![image](https://github.com/panchnayak/kubernetes-dev/blob/24cd08bde3e792925fa8c0f783226c33a08ed037/session-3/octant.jpg)

# Install MetalLB LoadBalancer for the Kubernetes Cluster.

```

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/metallb.yaml
# On first install only
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
  
$ kubectl get pods -n metallb-system
$ kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.9.6/manifests/example-layer2-config.yaml

# Its time to test the Load Balancer
  
$ kubectl apply -f nginx-deploy.yaml 
$ kubectl apply -f nginx-service.yaml 
$ kubectl get services
  
  MacBook-Pro:k8s pnayak$ kubectl get services
NAME            TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)        AGE
kubernetes      ClusterIP      10.96.0.1       <none>          443/TCP        37m
ngnix-service   LoadBalancer   10.103.190.81   192.168.1.240   80:32150/TCP   8s

```
Now opn your browser and try to access the nginx webserver using http://192.168.1.240:80 and you should get the homepage of NGINX webserver

