
kubectl create -f node-deployment.yaml

kubectl create -f node-service.yaml

kubectl delete -f node-deployment.yaml

kubectl delete -f node-service.yaml