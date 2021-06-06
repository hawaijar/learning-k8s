## Steps to run MiniKube cluster

<hr />

### First step:

Run the POD manifest file (yaml)

- This will run the pod(s) and registered their labels so as to identify later by services.

```
    kubctl apply -f deployment.yaml
```

### Second step:

Run the Service(s) manifest file (yaml)

```
    kubectl apply -f services.yaml
```

### Third step:

Check whether the containers inside the pod are running properly/working.

```
    kubectl exec -it webapp sh
    /# wget http://localhost:80
    /# cat index.html
```

### Fourth step

Access the service as shown below -

```
    curl http://127.0.0.1/30000
```

##### Note: Below applies to MacOS only.

For Mac, I found the above curl/browser not working. So Mac users, please follow below one!

```
minikube service --url fleetman-webapp
```

It'll return IP:Port of services (tunnel) as shown something like below -

```
🏃  Starting tunnel for service fleetman-webapp.
|-----------|-----------------|-------------|------------------------|
| NAMESPACE |      NAME       | TARGET PORT |          URL           |
|-----------|-----------------|-------------|------------------------|
| default   | fleetman-webapp |             | http://127.0.0.1:50011 |
|-----------|-----------------|-------------|------------------------|
```

### Final step(for Mac users only)

Run the service from curl/browser as shown below

```
    curl http://http://127.0.0.1:50011
```
