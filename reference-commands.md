# Kubernetes Deployment Scaling Command Reference Guide

### Project Content Table
- [Core Operations](#core-operations)
- [Deployment Management](#deployment-management)
- [Scaling Operations](#scaling-operations)
- [Monitoring and Verification](#monitoring-and-verification)
- [Cleanup Operations](#cleanup-operations)

> **Author**: [Md Toriqul Islam](https://linkedin.com/in/thetoriqul)  
> **Description**: Comprehensive guide for Kubernetes deployment scaling operations  
> **Learning Focus**: Mastering Kubernetes deployment management and scaling  
> **Note**: Review and understand each command before execution in your environment.

## Core Operations

### Initial Deployment Setup
```bash
# Create a new deployment with Nginx
kubectl create deployment nginx-deployment \
    --image=nginx:latest \
    --replicas=3 \
    --port=80

# Verify deployment creation
kubectl get deployment nginx-deployment
```

### Basic Deployment Information
```bash
# Get detailed deployment information
kubectl describe deployment nginx-deployment

# Check deployment status
kubectl rollout status deployment/nginx-deployment
```

## Deployment Management

### Pod Management
```bash
# List all pods in the deployment
kubectl get pods -l app=nginx-deployment

# Get detailed pod information
kubectl describe pods -l app=nginx-deployment

# Check pod logs
kubectl logs -l app=nginx-deployment
```

### ReplicaSet Management
```bash
# View ReplicaSets
kubectl get rs

# Describe ReplicaSet details
kubectl describe rs -l app=nginx-deployment
```

## Scaling Operations

### Manual Scaling
```bash
# Scale deployment to 7 replicas
kubectl scale deployment nginx-deployment --replicas=5

# Verify scaling operation
kubectl get deployment nginx-deployment
kubectl get pods -l app=nginx-deployment

# Scale down to 4 replicas
kubectl scale deployment nginx-deployment --replicas=2

# Verify scale-down
kubectl get pods -l app=nginx-deployment -w
```

### Advanced Scaling Options
```bash
# Record scaling command in revision history
kubectl scale deployment nginx-deployment --replicas=5 --record

# Scale multiple deployments
kubectl scale deployment nginx-deployment other-deployment \
    --replicas=6
```

## Monitoring and Verification

### Deployment Status
```bash
# Get deployment status
kubectl rollout status deployment/nginx-deployment

# View deployment history
kubectl rollout history deployment/nginx-deployment

# Check deployment events
kubectl get events --field-selector involvedObject.name=nginx-deployment
```

### Resource Monitoring
```bash
# Monitor pod creation/deletion
kubectl get pods -w

# Get resource usage
kubectl top pods -l app=nginx-deployment
```

## Cleanup Operations

### Deployment Cleanup
```bash
# Delete deployment
kubectl delete deployment nginx-deployment

# Verify cleanup
kubectl get all -l app=nginx-deployment
```

## Learning Notes

1. Always verify the current state before scaling operations
2. Monitor resource usage during scaling events
3. Use labels consistently for easy resource management
4. Maintain deployment history for rollback capability
5. Implement gradual scaling for production environments

---

> 💡 **Best Practice**: Always verify the deployment status after scaling operations

> ⚠️ **Warning**: Rapid scaling may impact cluster resources

> 📝 **Note**: Adjust resource requests/limits before scaling in production