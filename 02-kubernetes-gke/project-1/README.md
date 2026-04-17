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