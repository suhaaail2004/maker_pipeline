# Maker – Static Website

A production-ready static website with **Docker** containerisation, a **Jenkins CI/CD pipeline**, and **Kubernetes** deployment manifests.

---

## 📁 Project Structure

```
maker/
├── css/                    # Stylesheets
├── fonts/                  # Web fonts
├── images/                 # Static images
├── js/                     # JavaScript files
├── manifests/              # Kubernetes manifests
│   ├── deployment.yaml     # Deployment (rolling update, 2 replicas)
│   └── service.yaml        # ClusterIP Service
├── index.html              # Main HTML entry point
├── Dockerfile              # Nginx-based container image
├── .dockerignore           # Files excluded from Docker build context
├── Jenkinsfile             # Declarative CI/CD pipeline
├── .gitignore              # Files excluded from Git
└── README.md               # This file
```

---

## 🐳 Docker

### Build
```bash
docker build -t maker-website:latest .
```

### Run
```bash
docker run -d -p 8000:80 --name maker maker-website:latest
# Visit http://localhost:8000
```

---

## ⚙️ Jenkins CI/CD Pipeline

The [`Jenkinsfile`](Jenkinsfile) defines a **declarative pipeline** with 4 stages:

| # | Stage | Description |
|---|-------|-------------|
| 1 | **Checkout** | Pull source code from SCM |
| 2 | **Build and Test** | Run build & test commands |
| 3 | **Docker Build and Push** | Build image and push to registry |
| 4 | **Update Deployment File** | Inject new image tag into `manifests/deployment.yaml` |

### Configure before first run

Open `Jenkinsfile` and update:

```groovy
REGISTRY     = 'your-dockerhub-username'       // ← your Docker registry
DOCKER_CREDS = 'docker-credentials-id'         // ← Jenkins credential ID
```

---

## ☸️ Kubernetes Deployment

### Deploy
```bash
kubectl apply -f manifests/
```

### Verify
```bash
kubectl rollout status deployment/maker-deployment -n production
kubectl get pods -n production
kubectl get svc  -n production
```

---

## 📄 License

MIT – see [LICENSE](LICENSE) for details.
