# GKE Deployment Project

## Files
- `deployment.yaml` - Deploys hello-app with 3 replicas
- `service.yaml` - Exposes deployment via LoadBalancer

## Deploy
\`\`\`bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get service hello-service  # Wait for EXTERNAL-IP
\`\`\`

## Clean Up
\`\`\`bash
kubectl delete service hello-service
kubectl delete deployment hello-app
\`\`\`
