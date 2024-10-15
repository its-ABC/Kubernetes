# Kubernetes RBAC
 RBAC (Role-Based Access Control) is a way to manage who can do what in your Kubernetes cluster. It controls access to resources based on roles assigned to users or applications.

Here’s how it works, simply:

- **Roles**: Define what actions can be performed, like reading pods, creating services, or deleting deployments. There are two types:
  - **Role**: Used within a specific namespace.
  - **ClusterRole**: Used across the entire cluster or specific namespaces.

- **RoleBinding/ClusterRoleBinding**: These bind a role to users or groups, giving them the permissions defined in the role. 
  - **RoleBinding**: Ties a Role to users in a namespace.
  - **ClusterRoleBinding**: Ties a ClusterRole to users across the whole cluster.

### Example:
Let’s say you have a user who needs only to view (but not change anything) pods:
1. **Create a Role** that allows only "read" access to pods.
2. **Bind the Role** to the user using a `RoleBinding`.

In short, RBAC ensures the right people have the right permissions, making your cluster secure by limiting what users can do.

