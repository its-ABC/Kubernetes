
---

# NGINX Deployment YAML Configuration

This document provides a detailed explanation of the NGINX Deployment configuration in Kubernetes. The YAML defines a deployment that manages a set of NGINX Pods, providing key features like replication and rolling updates.

---
---

## 1. `apiVersion: apps/v1`

-  The `apps/v1` API version is used for deploying resources related to applications, such as Deployments, StatefulSets, and DaemonSets. In this case, it defines the Deployment object for managing multiple NGINX Pods.

---
---

## 2. `kind: Deployment`

-  This specifies that the object is a `Deployment`. Deployments manage the creation and scaling of Pods, as well as performing rolling updates to update the Pod’s containers without downtime.

---
---

## 3. `metadata`

-  Provides metadata for the Deployment, such as its name and labels. Metadata includes important identification information.

  - **`name: nginx-deployment`**  
    -  The Deployment is named `nginx-deployment`. This name is unique within the namespace and is used to manage the Deployment.

  - **`labels:`**
    - The `app: nginx` label is attached to the Deployment, helping to identify it and group related objects within the cluster.

---
---

## 4. `spec`

- This section contains the specifications for the Deployment, such as how many replicas should be created, which Pods to manage, and what template to use.

### a. `replicas: 3`

- The Deployment will ensure that 3 NGINX Pods are running at any given time. If a Pod fails or is terminated, Kubernetes will automatically create a new Pod to maintain 3 replicas.

### b. `selector`

- The `selector` is used to identify which Pods should be managed by the Deployment. It matches Pods with the `app: nginx` label.

  - **`matchLabels:`**
    - The Deployment will manage any Pods that have the `app: nginx` label.

---
---

### c. `template`

- Defines the Pod template used to create the Pods managed by the Deployment.


#### i. `metadata`

-  Each Pod created by the Deployment will be labeled with `app: nginx`, so they can be easily selected by the Deployment’s `selector`.

#### ii. `spec`

-  This section describes the container image, ports, and other settings for the Pods created by the Deployment.

  - **`containers:`**
    -  This field is an array, allowing multiple containers per Pod, but in this case, there is only one NGINX container.

    - **`- name: nginx`**  
      - **Description**:The container is named `nginx` and will be referenced as such in logs and debugging.

    - **`image: nginx:1.14.2`**  
      -  Specifies the Docker image and version to use for the container.

    - **`ports:`**
      - **Description**:The container will expose `port 80`, which is the standard port for HTTP traffic. Other services or Pods can connect to the NGINX server through this port.

        - **`- containerPort: 80`**  
          - **Description**:The container listens on port `80` for HTTP requests, allowing communication between Pods or external services.

---
---

This YAML configuration defines a Kubernetes Deployment that ensures 3 replicas of the NGINX Pods are running at all times, using the `nginx:1.14.2` image and exposing port 80 for HTTP traffic. The Deployment allows for automatic scaling, updates, and management of the Pods.



---

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