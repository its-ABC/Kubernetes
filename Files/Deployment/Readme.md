# Kubernetes NGINX Deployment Commands

This document outlines the Kubernetes commands used to manage the NGINX Deployment and demonstrates various aspects of Kubernetes such as deployment, scaling, updating, and cleanup.

---

## 1. Create the NGINX Deployment

```bash
kubectl apply -f nginx-deployment.yaml
```

- **Purpose**: This command applies the YAML configuration to your Kubernetes cluster. It creates a Deployment called `nginx-deployment`, which manages 3 replicas of NGINX Pods.

---

## 2. Check Deployment Status

```bash
kubectl get deployments
```

- **Purpose**: Lists all Deployments in the cluster. This allows you to verify that `nginx-deployment` has been successfully created and is managing the desired number of replicas.

---

## 3. Check Pods Created by the Deployment

```bash
kubectl get pods
```

- **Purpose**: Lists all Pods in the cluster, including those managed by the `nginx-deployment`. You should see 3 Pods running with names like `nginx-deployment-xxxx`.

---

## 4. Get Detailed Information about the Deployment

```bash
kubectl describe deployment nginx-deployment
```

- **Purpose**: Provides detailed information about the `nginx-deployment`, including its current state, events, conditions, and history. Useful for understanding the status of your deployment and any issues that might arise.

---

## 5. Get Detailed Information about a Specific Pod

```bash
kubectl describe pod <pod-name>
```

- **Purpose**: Replace `<pod-name>` with the name of one of the Pods (from the `kubectl get pods` output). This provides detailed information about that specific Pod, including events, container status, and configuration.

---

## 6. Scale the Deployment to 5 Replicas

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

- **Purpose**: Scales the number of replicas managed by the `nginx-deployment` from 3 to 5. This demonstrates Kubernetes’ ability to scale applications horizontally with ease.

---

## 7. Check Pods After Scaling

```bash
kubectl get pods
```

- **Purpose**: After scaling, this command will show 5 NGINX Pods running. It allows you to verify that scaling was successful.

---

## 8. Update the NGINX Image for a Rolling Update

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.0
```

- **Purpose**: Updates the NGINX image used by the `nginx-deployment` to version `1.16.0`. Kubernetes will perform a rolling update, replacing Pods one at a time without downtime.

---

## 9. Monitor the Rollout Status

```bash
kubectl rollout status deployment/nginx-deployment
```

- **Purpose**: Monitors the progress of the rolling update to ensure that all Pods are updated successfully. This command is useful for tracking the update in real-time.

---

## 10. Roll Back to the Previous Deployment Version (Optional)

```bash
kubectl rollout undo deployment/nginx-deployment
```

- **Purpose**: Reverts the `nginx-deployment` to its previous configuration (before the update to `nginx:1.16.0`). This is helpful if the update caused issues or is undesirable.

---

## 11. Delete the Deployment

```bash
kubectl delete deployment nginx-deployment
```

- **Purpose**: Deletes the `nginx-deployment`, which will also terminate all Pods managed by the Deployment. Use this command to clean up the cluster after the demonstration.

---

These commands form a comprehensive guide for showcasing the creation, management, scaling, and updating of an NGINX Deployment in Kubernetes.