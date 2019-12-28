# MYSQL + PHPMYADMIN in Kubernetes

## MYSQL

### create Persistent Volume
create a file named mysql-pv.yaml
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi

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
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  ports:
  - protocol: TCP
    port: 3306
    targetPort: 3306
  selector:
    app: mysql
  clusterIP: None
---
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: mysql
spec:
  selector:
    matchLabels:
      app: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - image: mysql:5.7
        name: mysql
        env:
          # Use secret in real usage
        - name: MYSQL_ROOT_PASSWORD
          value: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim
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


# PHPMYADMIN

### secret

create a file named phpmyadmin-secret.yaml
```
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secrets
type: Opaque
data:
  root-password: password
```

deploy
```
kubectl create -f phpmyadmin-secret.yaml
```

### deployment

create a file named phpmyadmin-deployment.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: phpmyadmin-deployment
  labels:
    app: phpmyadmin
spec:
  replicas: 1
  selector:
    matchLabels:
      app: phpmyadmin
  template:
    metadata:
      labels:
        app: phpmyadmin
    spec:
      containers:
        - name: phpmyadmin
          image: phpmyadmin/phpmyadmin
          ports:
            - containerPort: 80
          env:
            - name: PMA_HOST
              value: mysql # nome del servizio mysql
            - name: PMA_PORT
              value: "3306"
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-secrets
                  key: root-password
```

deploy file:
```
kubectl create -f deployment-phpmyadmin.yaml
```

### service
create a file named phpmyadmin-service.yaml
```
apiVersion: v1
kind: Service
metadata:
  name: phpmyadmin-service
spec:
  type: NodePort
  selector:
    app: phpmyadmin
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80 
```

deploy:
```
kubectl create -f phpmyadmin-service.yaml 
```

### delete

```
kubectl delete -f phpmyadmin/phpmyadmin-service.yaml

kubectl delete -f phpmyadmin/phpmyadmin-deployment.yaml

kubectl delete -f phpmyadmin/phpmyadmin-secret.yaml
```