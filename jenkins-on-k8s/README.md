## Install Jenkins on Kubernetes Cluster

```
$ kubectl apply -f jenkins-namespace.yaml
$ kubectl apply -f jenkins-volume.yaml

$ helm repo add jenkins https://charts.jenkins.io
$ helm repo update
$ helm search repo jenkins

$ wget https://raw.githubusercontent.com/jenkinsci/helm-charts/main/charts/jenkins/values.yaml

Edit values with 

runAsUser: 0

And Volume and VolumeClaim values



$ helm install jenkins -f values.yaml jenkins/jenkins  --namespace jenkins
$ printf $(kubectl get secret --namespace jenkins jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo

$ kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/chart-admin-password && echo

$ export POD_NAME=$(kubectl get pods --namespace jenkins -l "app.kubernetes.io/component=jenkins-master" -l "app.kubernetes.io/instance=jenkins" -o jsonpath="{.items[0].metadata.name}")

```
