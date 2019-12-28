# MYSQL in Kubernetes

### create Persistent Volume
create a file named mysql-pv.yaml
```
insert code

```

deploy configuration in kubernates:
```
kubectl apply -f mysql-pv.yaml

or

kubectl create -f mysql-pv.yaml

```

check if volumes is created:
```
kubectl get pv

kubectl describe pv mysql-pv-volume
```
### deployment

create a file named mysql-deployment.yaml
```
insert code
```
deploy:
```
kubectl create -f mysql-deployment.yaml
```

check if loaded:
```
kubectl get deployment

kubectl get pods

kubectl get svc

kubectl describe deployment mysql
```

enter in mysql shell:
```
kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -ppassword
```

### delete
```
kubectl delete deployment,svc mysql

kubectl delete pvc mysql-pv-claim

kubectl delete pv mysql-pv-volume
```

oppure

```
kubectl delete -f mysql-deployment.yaml

kubectl delete -f mysql-pv.yaml

```
