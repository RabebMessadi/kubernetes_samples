### MYSQL + PHPMYADMIN in Kubernetes

# secret

create a file named phpmyadmin-secret.yaml
```
code
```

deploy
```
kubectl create -f phpmyadmin-secret.yaml
```

# deployment

create a file named deployment-phpmyadmin.yaml
```
insert code
```

deploy file:
```
kubectl create -f deployment-phpmyadmin.yaml
```

# service
create a file named phpmyadmin-service.yaml
```
code 
```

deploy:
```
kubectl create -f phpmyadmin-service.yaml 
```