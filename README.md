# K8s

**Role**

1.Role defines what can be done to Kubernetes Resources.
2.Role contains one or more rules that represent a set of permissions.
3.Permissions are additive. There are no deny rules.
4.Roles are namespaced, meaning Roles work within the constraints of a namespace. It would default to the default namespace if none was specified.
5.After creating a Role, you assign it to a user or group of users by creating a RoleBinding.
Example
Here’s an example Role in the “default” namespace that can be used to grant read access to pods:


Kubernetes — RBAC — Role
ClusterRole

ClusterRole works the same as Role, but they are applied to the cluster as a whole.
ClusterRoles are not bound to a specific namespace. ClusterRole give access across more than one namespace or all namespaces.
After creating a ClusterRole, you assign it to a user or group of users by creating a RoleBinding or ClusterRoleBinding.
ClusterRoles are typically used with service accounts.
Because ClusterRoles are cluster-scoped, you can use ClusterRoles to control access to different kinds of resources than you can with Roles.

Cluster-scoped resources (e.g. Nodes, PersistentVolumes)
Non-resource endpoints (e.g./healthz).
Namespaced resources (e.g. Pods across the entire cluster), across all namespaces.
Default ClusterRole:

cluster-admin: Cluster wide super user.
admin: Full access within a Namespace.
edit: Read/write within a Namespace.
view: Read-only within a Namespace.
Example
Here is an example of a ClusterRole that can be used to grant read access to secrets in any particular namespace, or across all namespaces (depending on how it is bound):


Kubernetes — RBAC — ClusterRole
RoleBinding

Role Binding is used for granting permission to a Subject.
RoleBinding holds a list of subjects (users, groups, or service accounts), and a reference to the role being granted.
Role and RoleBinding are used in namespaced scoped.
RoleBinding may reference any Role in the same namespace.
After you create a binding, you cannot change the Role or ClusterRole that it refers to. If you do want to change the roleRef for a binding, you need to remove the binding object and create a replacement.
ClusterRole and RoleBinding are used provide access to more than one namespace or the whole cluster.

Example
Here is an example of a RoleBinding that grants the “pod-reader” Role to the user “jane” within the “default” namespace. This allows “jane” to read pods in the “default” namespace.


Kubernetes — RBAC — RoleBinding
RoleBinding can also reference a ClusterRole to grant the permissions defined in that ClusterRole to resources inside the RoleBinding’s namespace. This kind of reference lets you define a set of common roles across your cluster, then reuse them within multiple namespaces.


Kubernetes — RBAC — RoleBinding — ClusterRole
ClusterRoleBinding

ClusterRole and ClusterRoleBinding function like Role and RoleBinding, except they have wider scope.
RoleBinding grants permissions within a specific namespace, whereas a ClusterRoleBinding grants access cluster-wide and to multiple namespaces.
ClusterRoleBinding is binding or associating a ClusterRole with a Subject (users, groups, or service accounts).
Example
To grant permissions across a whole cluster, you can use a ClusterRoleBinding. The following ClusterRoleBinding allows any user in the group “manager” to read secrets in any namespace.


Kubernetes — RBAC — ClusterRoleBinding
Elements in RBAC Definition
Subjects
Subjects are nothing but a group of users, services, or team making an attempt at Kubernetes API. It defines what operations a user, service, or a group can perform.

Users: These are global, and meant for humans or processes living outside the cluster.
Groups: Set of users.
Service Accounts: Kubernetes uses service accounts to authenticate and authorize requests by pods to the Kubernetes API server. These are namespaced and meant for intra-cluster processes running inside pods.
Verbs
The set of operations that can be executed to the resources are called verbs. For examples, different verbs are get, watch, create, delete. Ultimately all of them are Create, Read, Update or Delete (CRUD) operations.

Resources
The set of Kubernetes API Objects available in the cluster are called Resources. For examples, Pods, Deployments, Services, Nodes, PersistentVolumes etc.

With RBAC, Cluster admins can specify application access, add/remove permissions, and limit resource visibility depending upon user’s role.

Use Cases: What to use When?
Use Role and a RoleBinding to scope security to a single namespace.
Use ClusterRole and RoleBinding to scope security to several or all namespaces.
Use ClusterRole and ClusterRoleBinding to scope security to all namespaces OR cluster-scoped resources.
If you want to define a role within a namespace, use a Role; if you want to define a role cluster-wide, use a ClusterRole.

Summary
RBAC in Kubernetes is the mechanism that enables you to configure fine-grained and specific sets of permissions that define how a given user, or group of users, can interact with any Kubernetes object in cluster, or in a specific Namespace of cluster.
