
![image 5](../../../assets/image%205.png)

Here is an example:

```YAML
# deployment.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: second-app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: second-app
      tier: backend
  template:
    metadata:
      labels:
      app: second-app
      tier: backend
      spec:
        containers:
          - name: second-nodejs
            image: YOUR-IMAGE-DOCKER:tag
```

```YAML
kubectl apply -f deployment.yml
```

  

Setup service file

```YAML
# service.yml

apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  type: LoadBalancer
  selector:
  app: second-app
  tier: backend # tier label can be ignored if you want to run multiples POD's on same service
  ports:
    - protocol: "TCP"
  port: 80
  targetPort: 8080

```

```YAML
kubectl apply -f service.yml
```

  

- How to delete services, pods and deployments?

```YAML
kubectl delete -f deployment.yml,service.yml
```

  

You can merge multiples `.yml` files

  

```yaml
# masterDeployment.yml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: second-app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: second-app
      tier: backend
  template:
    metadata:
      labels: 
        app: second-app
        tier: backend
    spec: 
      containers:
        - name: second-nodejs
          image: YOUR-IMAGE-DOCKER:tag

---

apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  type: LoadBalancer
  selector:
    app: second-app
    tier: backend # tier label can be ignored if you want to run multiples POD's on same service
  ports:
    - protocol: 'TCP'
      port: 80
      targetPort: 8080

```

  

- Check the health of container

```yaml
# deployment.yml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: second-app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: second-app
      tier: backend
  template:
    metadata:
      labels: 
        app: second-app
        tier: backend
    spec: 
      containers:
        - name: second-nodejs
          image: YOUR-IMAGE-DOCKER:tag
          imagePullPolicy: Always # That means if there is a new push from the image, even with the same version, this deploy runs again
          livenessProbe: 
            httpGet: 
              path: /
              port: 8080
            periodSeconds: 10
            initialDelaySeconds: 5

```

