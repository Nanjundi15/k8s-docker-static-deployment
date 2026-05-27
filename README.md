# 🚀 Kubernetes Static CDN Deployment using Docker & Minikube

A real-world hands-on DevOps project demonstrating containerization and deployment of a static CDN application using Docker, Kubernetes, and Minikube.

This project focuses on Kubernetes deployments, Docker image creation, NodePort services, volume mounting, and troubleshooting deployment issues in a cloud-native environment.

---

# 📌 Project Task / Problem Statement

## Task Given

Create and deploy a Kubernetes-based CDN application with the following requirements:

- Deploy a containerized static web application
- Use Kubernetes Deployment and Service
- Mount static files using volumes
- Expose the application externally using NodePort
- Use Docker image inside Minikube
- Ensure the application is accessible successfully

---

# 🎯 Objective

The main objective of this project was to gain practical experience in:

- Docker image creation
- Kubernetes deployment management
- Service exposure using NodePort
- Minikube cluster operations
- Volume mounting
- Troubleshooting Kubernetes deployment issues

---

# 🛠 Technologies Used

| Technology | Purpose |
|------------|---------|
| Docker | Containerization |
| Kubernetes | Container Orchestration |
| Minikube | Local Kubernetes Cluster |
| Nginx | Static Content Server |
| YAML | Kubernetes Configuration |
| Ubuntu Linux | Development Environment |

---

# 📂 Project Structure

```bash
k8s-docker-static-deployment/
│
├── deployment.yml
├── svc.yml
├── Dockerfile
├── README.md
└── data/
```

---

# 🐳 Step 1 — Create Dockerfile

## Dockerfile

```dockerfile
FROM nginx
COPY data /usr/share/nginx/html
```

## Explanation

- Used the official Nginx image
- Copied static content into Nginx HTML directory
- Built a lightweight CDN-style static server

---

# ☸ Step 2 — Create Kubernetes Deployment

## deployment.yml

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: cdn

spec:
  replicas: 1

  selector:
    matchLabels:
      app: cdn

  template:
    metadata:
      labels:
        app: cdn

    spec:
      containers:
      - name: cdn
        image: simple-cdn
        imagePullPolicy: Never

        ports:
        - containerPort: 80

        volumeMounts:
        - name: static-volume
          mountPath: /www

      volumes:
      - name: static-volume
        hostPath:
          path: /static
```

---

# 📝 How I Solved It

## What I Configured

### Deployment
- Created a Kubernetes Deployment named `cdn`
- Configured 1 replica
- Added labels and selectors

### Container
- Used custom Docker image `simple-cdn`
- Exposed port `80`

### Volume Mount
- Mounted static files using `hostPath`
- Connected `/static` to `/www`

---

# 🌐 Step 3 — Create Kubernetes Service

## svc.yml

```yaml
apiVersion: v1
kind: Service

metadata:
  name: cdn

spec:
  type: NodePort

  selector:
    app: cdn

  ports:
  - port: 80
    targetPort: 80
    nodePort: 32222
```

---

# 📝 How I Answered the Task

## Service Configuration

- Created Kubernetes Service named `cdn`
- Used `NodePort` type
- Exposed application externally on port `32222`

This allowed external access to the deployed application.

---

# 🚀 Step 4 — Start Docker

```bash
sudo service docker start
```

---

# 🚀 Step 5 — Start Minikube

```bash
minikube start --mount --mount-string="/home/ubuntu/code/data:/static" --driver=docker
```

## Explanation

- Started Minikube cluster
- Mounted local data directory into Minikube
- Enabled Kubernetes to access static files

---

# 🚀 Step 6 — Build Docker Image

```bash
docker build -t simple-cdn .
```

## Explanation

- Built custom Docker image
- Tagged image as `simple-cdn`

---

# 🚀 Step 7 — Load Image into Minikube

```bash
minikube image load simple-cdn
```

## Why This Was Important

Kubernetes inside Minikube could not access local Docker images directly.

This command loaded the image into the Minikube cluster.

---

# 🚀 Step 8 — Deploy Kubernetes Resources

## Apply Deployment

```bash
kubectl apply -f deployment.yml
```

## Apply Service

```bash
kubectl apply -f svc.yml
```

---

# 🚀 Step 9 — Verify Deployment

## Check Pods

```bash
kubectl get pods
```

Expected Output:

```bash
STATUS: Running
```

---

## Check Services

```bash
kubectl get svc
```

Expected Output:

```bash
32222/TCP
```

---

# 🔍 Problems Faced & Solutions

| Problem | Solution |
|---------|-----------|
| ErrImageNeverPull | Loaded image using Minikube |
| Dockerfile missing | Created custom Dockerfile |
| YAML validation errors | Corrected field names and indentation |
| NodePort issue | Fixed service configuration |
| URL check failed | Corrected image and deployment setup |

---

# 📚 Key Learnings

Through this project, I gained hands-on experience in:

- Kubernetes Deployments
- NodePort Services
- Docker Image Management
- Volume Mounting
- Kubernetes Troubleshooting
- Minikube Cluster Management
- Container Networking

---

# ✅ Final Result

✔ Deployment Created Successfully  
✔ Service Running Successfully  
✔ Pod Status Running  
✔ NodePort Accessible  
✔ URL Validation Passed  
✔ All Test Cases Passed

---

# 💡 Future Improvements

- Helm Charts
- CI/CD Pipeline using GitHub Actions
- Kubernetes Ingress
- Persistent Volumes
- Monitoring with Prometheus & Grafana

---

# 👨‍💻 Author

## Nanjundi K

Aspiring Software Engineer | DevOps & Cloud Enthusiast

Passionate about:
- Kubernetes
- Cloud Computing
- DevOps
- AI/ML
- Scalable Systems

---

# ⭐ Repository

## Repository Name

```bash
k8s-docker-static-deployment
```

If you found this project useful, feel free to star the repository and connect with me on LinkedIn.

---
