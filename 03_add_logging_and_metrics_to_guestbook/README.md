# Add logging and metrics to the PHP / Redis Guestbook example

part 1: https://kubernetes.io/docs/tutorials/stateless-application/guestbook/

part 2: https://kubernetes.io/docs/tutorials/stateless-application/guestbook-logs-metrics-with-elk/

# N.B:
examples is the original repository that I had cloned, but is not update with the last request of the last kubernetes request, so I copy it in beats with my custom update.

### create redis php guestbook
```
kubectl apply -f guestbook/redis-master-deployment.yaml 
kubectl logs -f redis-master-7db7f6579f-bv7ng
kubectl apply -f guestbook/redis-master-service.yaml 
kubectl apply -f guestbook/redis-slave-deployment.yaml 
kubectl apply -f guestbook/redis-slave-service.yaml 
kubectl apply -f guestbook/frontend-deployment.yaml 
kubectl get pods -l app=guestbook -l tier=frontend
kubectl get pods -l app=guestbook -l tier=backend
kubectl apply -f guestbook/frontend-service.yaml 
kubectl get services
minikube service frontend --url
kubectl get service frontend
kubectl scale deployment frontend --replicas=5
kubectl get service frontend
kubectl get pods
kubectl scale deployment frontend --replicas=2
kubectl get pods
```

### metrics
Create a cluster level role binding so that you can deploy kube-state-metrics and the Beats at the cluster level (in kube-system).

```
kubectl create clusterrolebinding cluster-admin-binding \
 --clusterrole=cluster-admin --user=pierangelo1982@gmail.com
```

insrall kube metrics
```
kubectl get pods --namespace=kube-system | grep kube-state

```


Clone the Elastic examples GitHub repo
```
git clone https://github.com/elastic/examples.git
```
