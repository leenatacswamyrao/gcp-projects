1. logged in into google skills booster
2. kubernetes in google cloud
3. gke qwiklabs
4. set the region and compute zones -->  gcloud config set compute/region asia-south1-a and gcloud config set compute/zone us-east4-b
5. create a gke cluster --> gcloud container clusters create --machine-type=e2-medium --zone=us-east4-b lab-cluster
6. authenticate the cluster --> gcloud container clusters get-credentials lab-cluster
7. deploy an application to the cluster -->  kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
8. expose application to external traffic --> kubectl expose deployment hello-server --type=LoadBalancer --port 8080
9. inspect the server -->kubectl get service
10. replace the external ip with the one in output from above step and open the url in browser --> http://<external ip>:8080
11. delete the cluster --> gcloud container clusters delete lab-cluster

# GCP Kubernetes Quest - Day 1

## Lab Completed
- Lab name: [Insert lab name]
- Date: April 10, 2025
- Duration: 45 minutes

## Key Learnings
- How to create a GKE cluster using gcloud CLI
- How to deploy applications to GKE
- kubectl basic commands

## Commands Used
- `gcloud container clusters create` - Create cluster
- `kubectl create deployment` - Deploy app
- `kubectl expose` - Create service
- `kubectl get pods` - List pods

## Screenshots
- [Include screenshot files]

# Google Cloud Platform Projects

## Project 1: GKE Deployments (April 10, 2026)

### Overview
Deployed applications to Google Kubernetes Engine using declarative YAML configurations.

### Labs Completed
1. Kubernetes Engine: Qwik Start
2. Deploying Applications to GKE

### Key Learnings
- Created GKE cluster using `gcloud container clusters create`
- Deployed applications using `kubectl apply -f deployment.yaml`
- Exposed applications using LoadBalancer service
- Scaled deployments using replicas

### Files
- `gke-deployments/deployment.yaml` - Deployment configuration
- `gke-deployments/service.yaml` - Service configuration

### Commands Used
\`\`\`bash
# Create cluster
gcloud container clusters create my-cluster --num-nodes=3

# Get credentials
gcloud container clusters get-credentials my-cluster

# Apply configurations
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# Verify
kubectl get deployments
kubectl get pods
kubectl get services
\`\`\`

### Screenshots
- [GKE Cluster Dashboard]
- [Running Pods]
- [External IP Access]
