## Tekton

```bash

$ kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml


$ kubectl create configmap config-artifact-pvc \
  --from-literal=size=10Gi \
  --from-literal=storageClassName=manual \
  -o yaml -n tekton-pipelines \
  --dry-run=client | kubectl replace -f -

$ brew tap tektoncd/tools
$ brew install tektoncd/tools/tektoncd-cli

$ kubectl apply --filename https://github.com/tektoncd/dashboard/releases/latest/download/tekton-dashboard-release.yaml

$ kubectl proxy --port=8080

```

### Access the dashboard

http://localhost:8080/api/v1/namespaces/tekton-pipelines/services/tekton-dashboard:http/proxy/


### ArgoCD

```bash

$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
$ kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
$ kubectl port-forward svc/argocd-server -n argocd 8080:443
```

###Octant

![image](https://user-images.githubusercontent.com/31803506/120935336-48b12c00-c6d0-11eb-91f1-5b2e930fecf7.png)
