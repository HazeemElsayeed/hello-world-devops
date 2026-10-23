# Hello World DevOps Project 🚀

A simple DevOps project demonstrating containerization, CI/CD automation, and Kubernetes deployment.

## 🛠️ Tech Stack

- **Git & GitHub** — Source code management
- **Docker** — Containerization
- **Docker Hub** — Container image registry
- **Jenkins** — CI/CD pipeline
- **Kubernetes** — Container orchestration
- **Minikube** — Local Kubernetes cluster
- **ConfigMap & Secret** — Configuration management
- **Horizontal Pod Autoscaler (HPA)** — Automatic scaling based on CPU utilization

## 🏗️ Architecture

1. Source code is stored in GitHub.
2. Jenkins builds a Docker image.
3. Jenkins pushes the image to Docker Hub.
4. Kubernetes deploys the image using a Deployment.
5. A NodePort Service exposes the application.
6. ConfigMap and Secret provide environment variables.
7. HPA adjusts the number of replicas based on CPU utilization.

## 📁 Project Structure

```text
hello-world-devops/
├── src/
│   └── index.html
├── Dockerfile
├── Jenkinsfile
├── deployment.yaml
├── service.yaml
├── configmap.yaml
├── secret.yaml
├── hpa.yaml
└── README.md
```

## ✅ Prerequisites

Install the following tools before running the complete project:

- Git
- Docker
- kubectl
- Minikube
- Jenkins (for the CI/CD pipeline)

## 🐳 Run with Docker

Clone the repository:

```bash
git clone https://github.com/HazeemElsayeed/hello-world-devops.git
cd hello-world-devops
```

Build the Docker image:

```bash
docker build -t hello-world-devops .
```

Run the container:

```bash
docker run -d --name hello-world-app -p 8080:80 hello-world-devops
```

Open the application in your browser:

http://localhost:8080

To stop and remove the container:

```bash
docker stop hello-world-app
docker rm hello-world-app
```

## ☸️ Deploy to Kubernetes with Minikube

Start Minikube:

```bash
minikube start --driver=docker
```

Apply the Kubernetes resources:

```bash
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f hpa.yaml
```

Check the deployment:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
kubectl get hpa
```

Enable the Metrics Server if it is not already enabled:

```bash
minikube addons enable metrics-server
```

Check resource usage:

```bash
kubectl top pods
```

Open the application:

```bash
minikube service hello-world-service
```

The HPA targets 50% average CPU utilization and scales between 2 and 5 replicas. Scaling depends on resource availability and actual workload.

## ⚙️ Jenkins CI/CD Pipeline

The `Jenkinsfile` defines a pipeline that:

1. Builds the Docker image.
2. Authenticates with Docker Hub using Jenkins Credentials.
3. Pushes the image to Docker Hub.

### Jenkins Setup

1. Install and start Jenkins.
2. Create a Pipeline job.
3. Configure the job to use **Pipeline script from SCM**.
4. Select Git as the SCM.
5. Set the repository URL to:

   `https://github.com/HazeemElsayeed/hello-world-devops.git`

6. Set the branch to `*/main`.
7. Set the Script Path to `Jenkinsfile`.
8. Add a Jenkins username/password credential with the ID `dockerhub-credentials`.
9. Use your own Docker Hub username and access token for the credential.
10. Run the pipeline.

**Note:** The Jenkins pipeline builds and pushes the image. Kubernetes deployment is a separate step in the current implementation.

## 🔐 Security Notes

- Never commit real passwords, API tokens, or production secrets to GitHub.
- The `secret.yaml` file is intended for demonstration only. Replace the sample secret with a secure approach before using this project beyond local testing.
- Kubernetes Secrets are not automatically encrypted at rest in every cluster configuration.
- Use your own credentials when configuring Jenkins.

## 👤 Author

**Hazeem Elsayeed**

GitHub: https://github.com/HazeemElsayeed
