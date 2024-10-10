
# NGINX Pod YAML Configuration

### 1. `apiVersion: v1`

     - Specifies the API version used for this object definition.  


### 2. `kind: Pod`
     Defines the type of Kubernetes object.  


### 3. `metadata:`
     Provides metadata for the Pod, such as its name.Metadata contains important information about the Pod, including how it can be identified within the cluster. In this case, metadata only includes the Pod's name.

- **`name: nginx`**  
     The name given to the Pod. The Pod is named `nginx`. This name must be unique within the same namespace in Kubernetes. The name helps in identifying and managing the Pod when running various `kubectl` commands like `kubectl get pods` or `kubectl delete pod nginx`.

### 4. `spec:`
     This is where we describe what the Pod should look like. It contains details about the containers that will be running in this Pod, including images and ports.

- **`containers:`**  
     Defines the list of containers that will run inside the Pod. Every Pod must have at least one container, but it can run multiple containers. The `containers` field is an array, and in this case, only one container is specified.

  - **`- name: nginx`**  
     This container is named `nginx`. The name should be unique within the Pod but can be the same across different Pods. It is helpful for referring to this container in logs or debugging.

  - **`image: nginx:1.14.2`**  
     The container will run using the `nginx` image from Docker Hub, specifically version `1.14.2`. The image is pulled from the default Docker registry unless otherwise specified. NGINX is a popular web server used for hosting websites and web services.

  - **`ports:`**  
     A container can expose one or more ports to enable communication with the outside world or other containers. This field lists the container ports that need to be exposed.

    - **`- containerPort: 80`**  
      The container is exposing port `80`, which is the standard port for HTTP traffic. This allows access to the NGINX server from other Pods or services that might want to communicate with it.


## Commands for Execution


### 1. Deploy the Pod

```bash
kubectl apply -f nginx-pod.yaml
```
**Purpose**: This command applies the YAML configuration and creates the NGINX Pod in your Kubernetes cluster. The Pod will run using the `nginx:1.14.2` image, exposing port 80.

---

### 2. Check the Status of the Pod

```bash
kubectl get pods
```
**Purpose**: This command lists all running Pods in your cluster. After running it, you should see a Pod named `nginx` in the list with a status of `Running` if everything is working correctly.

---

### 3. Get Detailed Pod Information

```bash
kubectl describe pod nginx
```
**Purpose**: This command provides detailed information about the `nginx` Pod, including:
- Events (such as creation, scheduling, and container start)
- Pod status
- Container configuration
- Any errors or warnings

This is useful for troubleshooting if the Pod isn't behaving as expected or if you want detailed logs for debugging.

---

### 4. Delete the Pod

```bash
kubectl delete pod nginx
```
**Purpose**: This command deletes the `nginx` Pod from your Kubernetes cluster. You can run this when you no longer need the Pod.

---

