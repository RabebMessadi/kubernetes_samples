
create:
```
kubectl create -f node-deployment.yaml
```
```
kubectl create -f node-service.yaml
```
Delete:
```
kubectl delete -f node-deployment.yaml
```

```
kubectl delete -f node-service.yaml
```

Scale:
```
kubectl scale deployment node-hostname --replicas=5
```

Check:
```
minikube service list
```