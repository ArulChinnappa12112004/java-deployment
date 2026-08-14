# 1. Create the namespace if it doesn't exist
kubectl create namespace java-demo --dry-run=client -o yaml | kubectl apply -f -

# 2. Apply Configs, Secrets, and Storage
kubectl apply -f postgres-config.yaml -f postgres-pvc.yaml -f java-config.yaml

# 3. Apply PostgreSQL Workload & Service
kubectl apply -f postgres-deployment.yaml -f postgres-service.yaml

# 4. Apply Java App Workload & Service
kubectl apply -f java-deployment.yaml -f java-service.yaml

# 5. Apply Adminer Deployment and Service 
kubectl apply -f adminer-deployment.yaml

# 6. Port forward
kubectl port-forward svc/adminer-service -n java-demo 8080:8080

# Java Demo Application Stack on Docker Desktop Kubernetes

This directory contains the Kubernetes manifests to run PostgreSQL 17, a Java Spring Boot backend, and Adminer DB web client inside Docker Desktop Kubernetes on macOS.

## Quick Start (Deploying Everything)

Run Kustomize directly through `kubectl` from inside the `k8s/` directory:

```bash
kubectl apply -k .

see i have two repo one is java-application and another is java-deployment , i changed the version in the (java-deployment: java-deployment.yml) using github action by java-application repo , when ever i created a tag that is new realise, the changes happened.
now I want to put the java-deployment changes in the aws cloud which i created. I created a EC2 instance in aws and put sudo apt-get update

sudo apt-get install -y ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install -y \
  docker-ce \
  docker-ce-cli \
  containerd.io \
  docker-buildx-plugin \
  docker-compose-plugin
Ensure current user added to docker grouo
sudo usermod -aG docker $USER
newgrp docker
docker ps
Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s \
  https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
rm kubectl
install kind cluster
curl -Lo ./kind \
  https://kind.sigs.k8s.io/dl/v0.30.0/kind-linux-amd64

chmod +x ./kind

sudo mv ./kind /usr/local/bin/kind
check kind version
kind version, now i want to push that changes in kind cluster using github actions give each and every steps to complete the task



