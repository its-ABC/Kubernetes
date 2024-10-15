# ConfigMap & Secrets
In Kubernetes, **ConfigMap** and **Secrets** are used to manage configuration data and sensitive information separately from the application code. This separation allows you to easily update configurations or credentials without rebuilding your application images.

### 1. **ConfigMap**:
A **ConfigMap** is an object used to store non-sensitive configuration data in key-value pairs. It's typically used for storing configuration settings that your applications might need, such as environment variables, config files, or command-line arguments.

### **Working Principle of ConfigMap**:
- ConfigMaps decouple configuration data from your containerized applications.
- The configuration can be injected into pods as environment variables or mounted as files into the containers.
- ConfigMaps are not encrypted, so they should only be used for non-sensitive data.


---

### 2. **Secrets**:
A **Secret** is used to store sensitive information such as passwords, OAuth tokens, or SSH keys. Like ConfigMaps, Secrets hold data in key-value pairs, but the data in Secrets is base64-encoded and can be configured to be encrypted at rest, providing an additional level of security compared to ConfigMaps.

### **Working Principle of Secrets**:
- Secrets store sensitive information and are more secure than ConfigMaps.
- They can be injected into pods as environment variables or mounted as files into the containers.
- Kubernetes avoids writing secrets to disk to reduce the chances of leaks, and they can be encrypted at rest using additional Kubernetes configurations.




---

### **Key Differences Between ConfigMap and Secrets**:
| Feature         | **ConfigMap**                                       | **Secret**                                        |
|-----------------|-----------------------------------------------------|---------------------------------------------------|
| **Purpose**     | Store non-sensitive configuration data.              | Store sensitive data (like passwords, tokens).    |
| **Data Storage**| Plain text, not encoded or encrypted.                | Base64-encoded, can be encrypted at rest.         |
| **Use Cases**   | Environment variables, configuration files.          | Passwords, API keys, tokens.                      |
| **Security**    | Not meant for sensitive data, stored as-is.          | More secure, with options for encryption.         |

### **Summary of Working Principles**:
- **ConfigMaps** allow you to externalize your application's configuration without rebuilding the container image.
- **Secrets** securely store sensitive data, ensuring that sensitive values are not hardcoded into your application or stored in plain text.

