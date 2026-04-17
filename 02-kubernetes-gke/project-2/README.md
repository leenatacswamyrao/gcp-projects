# GKE Flask App Deployment Project

A production-ready template for deploying a Python Flask application to Google Kubernetes Engine (GKE) Autopilot.

## 📁 Project Structure

* **app.py**: Flask application with `/` and `/health` endpoints.
* **requirements.txt**: Python dependencies (Flask, Gunicorn).
* **Dockerfile**: Multi-stage build for a lightweight container image.
* **deployment.yaml**: K8s Deployment with Autopilot-compliant resource requests.
* **service.yaml**: K8s Service (Type: LoadBalancer) for public access.

## 🚀 Deployment Workflow

### 1. Environment Preparation
```bash
export PROJECT_ID="gke-project-041123"
export REPO_NAME="test-repo"
export REGION="us-central1"

gcloud config set project $PROJECT_ID
gcloud auth configure-docker $REGION-docker.pkg.dev
```

### 2. Build and Push Image
Using Google Artifact Registry (Modern Standard):
```bash
docker build -t $REGION-docker.pkg.dev/$PROJECT_ID/$REPO_NAME/flask-app:v1 .
docker push $REGION-docker.pkg.dev/$PROJECT_ID/$REPO_NAME/flask-app:v1
```

### 3. Kubernetes Deployment
```bash
# Apply the deployment and load balancer
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# Monitor the rollout
kubectl get pods -w
```

## ⚙️ Management & Cost Optimization

To avoid consuming credits when the app is not in use:

* **Scale to Zero**: `kubectl scale deployment flask-app --replicas=0`
* **Remove Load Balancer**: `kubectl delete service flask-service`
* **Delete Cluster**: `gcloud container clusters delete flask-cluster --region $REGION`

## 💡 Lessons Learned
* **Registry Paths**: Always use `pkg.dev` for Artifact Registry to avoid `404` errors common with legacy `gcr.io`.
* **Probes**: Liveness and Readiness probes are essential for GKE to manage container health automatically.
* **Autopilot Resources**: Autopilot requires explicit `requests` in the YAML to schedule pods correctly.
