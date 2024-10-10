
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


# Commands for execution

- '''
kubectl apply -f pod.yaml
  '''
This command creates the NGINX Pod in your Kubernetes cluster based on the configuration in the YAML file.

- '''
kubectl get pods
  '''
Displays a list of running Pods in your cluster. You should see the Pod named 'nginx' with the status 'Running'.

- '''
kubectl describe pod nginx
  '''
Provides detailed information about the nginx Pod, including events, status, container information, and any errors or warnings that occurred during the creation of the Pod. Also used for debugging.

- '''
kubectl delete pod nginx
  '''
Removes the NGINX Pod from your Kubernetes cluster