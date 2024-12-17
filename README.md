გავუშვი Minikube-ის Kubernetes კლასტერი:

```bash
minikube start
```

შევამოწმე, რომ Minikube მუშაობს:

```bash
minikube status
```

### **Kubernetes კონფიგურაციის ფაილების შექმნა.**

     შევქმენი ახალი დირექტორია ფაილებისთვის:

```bash
mkdir kubernetes-nginx
cd kubernetes-nginx
```

გავაკეთე Deployment YAML ფაილი (`nginx-deployment.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

გავაკეთე Service YAML ფაილი (`nginx-service.yaml`):

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort

```

### **Deployment და Service-ის შექმნა**

     გავუშვი Deployment და Service:

```bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
```

Deployment და Service-ის შემოწმება:

```bash
kubectl get deployments
kubectl get services
kubectl get pods
```

![nginx](https://github.com/user-attachments/assets/1f358db6-6067-4ce6-ac34-59cc06d6668c)


### **აპლიკაციის გახსნა ბრაუზერში**

     Nginx-ის სერვისზე წვდომა გავაკეთე:

```bash
minikube service nginx-service
```

![nginx-service.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b912a3bd-dcf9-4e79-ba58-633f57c9dfaf/6172c8a6-02cb-4262-a46a-1e3ea6f8dfdb/nginx-service.png)

### **რესურსების გაწმენდა**

     წავშალე რესურსები:

```bash
kubectl delete -f nginx-deployment.yaml
kubectl delete -f nginx-service.yaml
```

და ბოლოს გავაჩერე Minikube:

```bash
minikube stop
```

s
