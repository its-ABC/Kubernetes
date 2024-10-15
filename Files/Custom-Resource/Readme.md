# Custom Resource
In Kubernetes, **Custom Resources (CRs)** are extensions of the Kubernetes API that allow you to create and manage your own resource types in addition to the built-in ones like Pods, Services, and Deployments. They let you define your own objects that Kubernetes can handle just like any other standard resource.

---

### 1. **CustomResourceDefinition (CRD)**
 The CRD is the blueprint for creating your custom resource. It defines the schema (structure) of the resource and tells Kubernetes how to understand and validate the custom objects you're going to create. Once the CRD is applied to the cluster, users can create instances of the resource.


### 2. **Custom Resource (CR)**
- The CR is an actual instance of the resource defined by the CRD. It represents a specific object based on the custom schema you defined in the CRD.


### 3. **Controllers**
- it watch for changes in resource (builtin & custom) and take action to match the current state with the desired state.

---

