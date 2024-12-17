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

![nginx-service](https://github.com/user-attachments/assets/2a25f2c7-6c35-4d86-933f-5e0da6b22e36)


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
