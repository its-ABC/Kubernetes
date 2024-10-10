


---

# NGINX Pod YAML Configuration



---

### 1. 
```bash
apiVersion: v1
```

- **Description**: Specifies the API version used for this object definition.Kubernetes uses different API versions for various objects. `v1` is one of the stable API versions, commonly used for core resources like Pods.

---

### 2. `kind: Pod`

- **Description**: Defines the type of Kubernetes object. Here, the `kind` is set to `Pod`, which represents the smallest and most basic unit in the Kubernetes object model. A Pod consists of one or more containers, which are logically grouped to work together.

---

### 3. `metadata:`

- **Description**: Provides metadata for the Pod, such as its name. Metadata helps identify and manage the Pod within the Kubernetes cluster.

  - **`name: nginx`**  
    - **Description**: The name given to the Pod.The Pod is named `nginx`, and this name must be unique within the same namespace in Kubernetes. You will use this name in various `kubectl` commands, such as checking the status of the Pod or deleting it.

---

### 4. `spec:`

- **Description**: Describes the desired state of the Pod.The `spec` section specifies what the Pod should look like and how it should behave. This includes information about the containers that will run inside the Pod.

  - **`containers:`**  
    - **Description**: Defines the list of containers that will run inside the Pod. Every Pod must have at least one container, but it can run multiple containers. The `containers` field is an array, and in this case, only one container is defined.

    - **`- name: nginx`**  
      - **Description**: The name of the container.This container is named `nginx`. The name should be unique within the Pod but can be the same across different Pods. This is useful when referring to the container in logs or debugging processes.

    - **`image: nginx:1.14.2`**  
      - **Description**: Specifies the Docker image & version used by the container.

    - **`ports:`**  
      - **Description**: This field specifies which container ports should be exposed to allow communication with the outside world or other services in the cluster.

        - **`- containerPort: 80`**  
          - **Description**: This specifies that the container will listen on port `80`, which is the standard port for HTTP traffic. Other Pods or services can communicate with this NGINX server through this port.

---

This YAML configuration defines a single NGINX container inside a Kubernetes Pod, specifying its image version and exposing port 80 for HTTP traffic.


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

