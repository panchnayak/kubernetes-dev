### Install ArgoCD on Kubernetes

```bash

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
```

### Change the argocd-server service type to LoadBalancer:

```bash

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
![image](https://user-images.githubusercontent.com/31803506/124612918-b754e700-de40-11eb-9b12-be31da197ac7.png)
