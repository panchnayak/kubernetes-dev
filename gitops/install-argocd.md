### Install ArgoCD on Kubernetes

```bash

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
```

### Change the argocd-server service type to LoadBalancer:

```bash

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
Now you can login to the argo cd server using the browser

Username is admin
You can get the password using the following command

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Install argocd CLI and login using argocd cli
```bash
argocd login "argocd server IP or domainame"
```
Change the password

```bash
argocd account update-password
```
