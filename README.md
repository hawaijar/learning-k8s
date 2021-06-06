## How to apply new version of webapp

### 1. Update the label of the service to include version number also
Update the deployment.yaml as shown below -

```
   ...
    labels:
    app: webapp
    release: "0.0"
   ...
```
Add another configuration for the new version (0.5) as shown below -
```
apiVersion: v1
kind: Pod
metadata:
  name: webapp-0.5
  labels:
    app: webapp
    release: "0.5"
spec:
  containers:
    - name: webapp
      image: richardchesterwood/k8s-fleetman-webapp-angular:release0-5
```

### 2. Update the service manifest (YAML) to point to the new version
```
spec:
  ...
  selector:
    app: webapp
    release: "0.5"
  ...
```

### 3. Apply both manifest files
```
    kubectl apply -f deployment.yaml
```
```
    kubectl apply -f services.yaml
```

### 4. Check whether the service points to new version
```
    kubectl describe service fleetman-webapp
```
You'll see output similar to something below -
```
Name:                     fleetman-webapp
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=webapp,release=0.5
Type:                     NodePort
IP:                       10.102.217.123
Port:                     http  80/TCP
TargetPort:               80/TCP
NodePort:                 http  30000/TCP
Endpoints:                172.18.0.4:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

As we can see above, service is now pointing to later version fo the webapp (release 0.5)
