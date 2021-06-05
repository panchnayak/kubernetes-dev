cd /home/pnayak/k8s

clone the Vagrantfile repo

$ vagrant up


$ vagrant ssh master

mkdir -p $HOME/.kube
sudo cp -Rf /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl cluster-info
kubectl get nodes

Install kubernetes dashboard dashboard

$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.2.0/aio/deploy/recommended.yaml

Access dashboard using proxy

$kubectl proxy

Access ui using
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard

Get the token by the following command

$ kubectl -n kube-system describe secret default

Install MetalLB

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/metallb.yaml
# On first install only
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
![image](https://user-images.githubusercontent.com/31803506/120892765-d7914c00-c5dd-11eb-820f-8a6da94a49c9.png)
