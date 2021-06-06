
## Install Spark on Kubernetes

```
$ ./bin/docker-image-tool.sh -r panchaleswar -t latest build

or

$SPARK_HOME/bin/docker-image-tool.sh -r panchaleswar -t v3.0.1-j14 \
-p kubernetes/dockerfiles/spark/bindings/python/Dockerfile -b java_image_tag=14-slim build


kubectl create serviceaccount spark
kubectl create clusterrolebinding spark-role --clusterrole=edit  --serviceaccount=default:spark --namespace=default

./spark-submit \
--master k8s://https://192.168.99.141:8443 \
--deploy-mode cluster \
--name spark-pi \
--class org.apache.spark.examples.SparkPi \
--conf spark.executor.instances=2 \
--conf spark.kubernetes.container.image=panchaleswar/spark:latest \
--conf spark.kubernetes.container.image.pullPolicy=Never \
--conf spark.kubernetes.authenticate.driver.serviceAccountName=spark \
local:///opt/spark/examples/jars/spark-examples_2.12-3.1.1.jar 10000000


./bin/spark-submit --master k8s://https://192.168.99.141:8443 --deploy-mode cluster --name spark-pi --class org.apache.spark.examples.SparkPi --conf spark.executor.instances=2 --conf spark.kubernetes.container.image=panchaleswar/spark:latest --conf spark.kubernetes.container.image.pullPolicy=Never --conf spark.kubernetes.authenticate.driver.serviceAccountName=spark local:///opt/spark/examples/jars/spark-examples_2.12-3.1.1.jar 10000000


kubectl port-forward spark-pi-0934d079bec33822-driver 4040:4040

```
