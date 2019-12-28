# Add logging and metrics to the PHP / Redis Guestbook example

part 1: https://kubernetes.io/docs/tutorials/stateless-application/guestbook/

part 2: https://kubernetes.io/docs/tutorials/stateless-application/guestbook-logs-metrics-with-elk/

### N.B:
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

command 2
```
minikube delete
minikube start --vm-driver=<driver_name>
minikube start --vm-driver=virtualbox
kubectl create -f redis-master-deployment.yaml
kubectl get pods
kubectl create -f redis-master-service.yaml 
kubectl create -f redis-slave-deployment.yaml 
kubectl create -f redis-slave-service.yaml 
kubectl create -f frontend-deployment.yaml 
kubectl create -f frontend-service.yaml 
kubectl get pods
kubectl get services
kubectl get pods
kubectl get services
kubectl get pods
cd ..
cd beats/
kubectl get pods
kubectl create clusterrolebinding cluster-admin-binding  --clusterrole=cluster-admin --user=pierangelo1982@gmail.com
kubectl get pods --namespace=kube-system | grep kube-state
kubectl create -f examples/standard
cd ..
kubectl create -f examples/standard
kubectl get pods -n kube-system -l app.kubernetes.io/name=kube-state-metrics
kubectl get pods --namespace=kube-system | grep kube-state-metrics
git clone https://github.com/kubernetes/kube-state-metrics.git kube-state-metrics
rm -rf kube-state-metrics/
git clone https://github.com/kubernetes/kube-state-metrics.git kube-state-metrics
kubectl create -f examples/standard
kubectl create -f kube-state-metrics/examples/standard/
kubectl get pods --namespace=kube-system | grep kube-state-metrics
kubectl get pods -n kube-system -l app.kubernetes.io/name=kube-state-metrics
kubectl create secret generic dynamic-logging   --from-file=./ELASTICSEARCH_HOSTS   --from-file=./ELASTICSEARCH_PASSWORD   --from-file=./ELASTICSEARCH_USERNAME   --from-file=./KIBANA_HOST   --namespace=kube-system
cd beats/
kubectl create secret generic dynamic-logging   --from-file=./ELASTICSEARCH_HOSTS   --from-file=./ELASTICSEARCH_PASSWORD   --from-file=./ELASTICSEARCH_USERNAME   --from-file=./KIBANA_HOST   --namespace=kube-system
kubectl create -f filebeat-kubernetes.yaml
kubectl get pods -n kube-system -l k8s-app=filebeat-dynamic
kubectl create -f metricbeat-kubernetes.yaml
kubectl get pods -n kube-system -l k8s-app=metricbeat
kubectl get pods -n kube-system -l k8s-app=filebeat-dynamic
kubectl create -f packetbeat-kubernetes.yaml
kubectl get pods -n kube-system -l k8s-app=packetbeat-dynamic
kubectl get pods -n kube-system
kubectl get pods
kubectl get pods -n kube-system
minikube service list

```

delete al namespace presence:
```
kubectl delete all --all -n kube-system
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

```
kubectl describe pod filebeat-dynamic-m2zwr --namespace kube-system
```
