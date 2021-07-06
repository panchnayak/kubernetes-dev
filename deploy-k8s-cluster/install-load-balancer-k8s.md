## How to install MetalLB load balancer to your kubernetes Cluster

### Install MetalLB

```bash

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/metallb.yaml

# For fisttime when you install the Load Balancer 

kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
kubectl get pods -n metallb-system
wget https://raw.githubusercontent.com/google/metallb/v0.9.6/manifests/example-layer2-config.yaml
```

### Edit example-layer2-config.yaml

```bash

vi example-layer2-config.yaml

apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: my-ip-space
      protocol: layer2
      addresses:
      - 192.168.1.150-192.168.1.250
```
Now you can create your services with type as "LoadBalancer"

```
apiVersion: v1
kind: Service
metadata:
  name: ngnix-service
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```
