## This is how you install a Kafka Cluser on Kubernetes

Open the application to outside traffic

Associate this application with the Istio gateway:

$ kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml

Ensure that there are no issues with the configuration:

$ istioctl analyze

Execute the following command to determine if your Kubernetes cluster is running in an environment that supports external load balancers:


$ kubectl get svc istio-ingressgateway -n istio-system

Follow these instructions if your environment does not have an external load balancer and choose a node port instead.

$ export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')

export SECURE_INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].nodePort}')


$ export INGRESS_HOST=$(kubectl get po -l istio=ingressgateway -n istio-system -o jsonpath='{.items[0].status.hostIP}')


Set GATEWAY_URL:

$ export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT

$ echo "http://$GATEWAY_URL/productpage"

http://192.168.26.21:30601/productpage


View the Istio Dashboard

$ kubectl apply -f samples/addons

$ kubectl rollout status deployment/kiali -n istio-system

$ istioctl dashboard kiali
![image](https://user-images.githubusercontent.com/31803506/120935149-5dd98b00-c6cf-11eb-9998-aed5eabcfd71.png)
