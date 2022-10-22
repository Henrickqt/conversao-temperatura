# Application

This is a web application used convert temperature, using Node. The main goal is to reproduce the use of Kubernetes, orchestrating Docker images with the K3D tool.

# How to run

## Prerequisites

In this case, we are using Windows:

- WSL2
- Docker Desktop
- Chocolatey

## Install k3d and kubernetes-cli

On terminal, as admin, input the followings commands:

```bash
choco install k3d
choco install kubernetes-cli
```

## Docker image creation

On terminal, as admin, input the followings commands:

```bash
git clone https://github.com/Henrickqt/conversao-temperatura.git
cd .\conversao-temperatura\src\

docker build -t henrickp/conversao-temperatura:v1 -f .\Dockerfile .
docker push henrickp/conversao-temperatura:v1

docker tag henrickp/conversao-temperatura:v1 henrickp/conversao-temperatura:latest
docker push henrickp/conversao-temperatura:latest
```

## Cluster creation

On terminal, as admin, input the followings commands:

```bash
cd ..\k8s\
k3d cluster create mycluster -p "80:30000@loadbalancer"
kubectl apply -f .\deployment.yaml
```

Wait till everything has been created. You can track it with the following command:

```bash
kubectl get pod
```

When at least one pod is with status 'Running', you can navigate to:
http://localhost/
