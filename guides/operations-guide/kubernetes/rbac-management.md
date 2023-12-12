---
description: Role-based access control
---

# RBAC Management

## Overview

Role-based access control (RBAC) regulates access to a computer or network resources based on the roles of individual users within your organization.

RBAC authorization uses the rbac.authorization.k8s.io API group to drive authorization decisions, allowing you to configure policies through the Kubernetes API dynamically.

### API objects[ ](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#api-overview) <a href="#api-overview" id="api-overview"></a>

The RBAC API declares four Kubernetes objects: _Role_, _ClusterRole_, _RoleBinding_ and _ClusterRoleBinding_. You can [describe objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/#understanding-kubernetes-objects), or amend them, using tools such as `kubectl`, just like any other Kubernetes object.

{% hint style="warning" %}
**Caution:** These objects, by design, impose access restrictions. If you are making changes to a cluster as you learn, see [privilege escalation prevention and bootstrapping](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#privilege-escalation-prevention-and-bootstrapping) to understand how those restrictions can prevent you from making some changes.
{% endhint %}

### Role & ClusterRole <a href="#role-and-clusterrole" id="role-and-clusterrole"></a>

An RBAC _Role_ or _ClusterRole_ contains rules that represent a set of permissions. Permissions are purely additive (there are no "deny" rules).

A Role always sets permissions within a particular [namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces); when you create a Role, you have to specify the namespace it belongs in.

ClusterRole, by contrast, is a non-namespaced resource. The resources have different names (Role and ClusterRole) because a Kubernetes object always has to be either namespaced or not namespaced; it can't be both.

ClusterRoles have several uses. You can use a ClusterRole to:

1. define permissions on namespaced resources and be granted access within individual namespace(s)
2. define permissions on namespaced resources and be granted access across all namespaces
3. define permissions on cluster-scoped resources

If you want to define a role within a namespace, use a Role; if you want to define a role cluster-wide, use a ClusterRole.

#### **ClusterRole In DIGIT**[ ](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#clusterrole-example)

A ClusterRole can be used to grant the same permissions as a Role. Because ClusterRoles are cluster-scoped, you can also use them to grant access to:

* cluster-scoped resources (like [nodes](https://kubernetes.io/docs/concepts/architecture/nodes/))
* non-resource endpoints (like `/healthz`)
*   namespaced resources (like Pods), across all namespaces

    For example: you can use a ClusterRole to allow a particular user to run `kubectl get pods --all-namespaces`

Here is the Digit [ClusterRole](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/helm/charts/cluster-configs/templates/rbac/clusterroles.yaml) that can be used to grant read access and restricted admin access

{% code lineNumbers="true" %}
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: digit-user
rules:
- apiGroups:
  - "extensions"
  resources:
  - deployments
  verbs:
  - patch
- apiGroups:
  - ""
  resources:
  - pods/portforward
  - pods/proxy 
  verbs:
  - create  
  - delete
---  
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: digit-admin
rules:
- apiGroups:
  - ""
  resources:
  - pods/portforward
  - pods/proxy 
  - pods/exec 
  verbs:
  - create  
  - delete
- apiGroups:
  - "batch"
  resources:
  - jobs 
  verbs:
  - create  
  - update
  - patch
  - list
- apiGroups: 
  - "apps"
  - "extensions"  
  resources: 
  - deployments
  verbs: 
  - patch 
  - get 
  - list
  - update    
```
{% endcode %}

### RoleBinding & ClusterRoleBinding

A role binding grants the permissions defined in a role to a user or set of users. It holds a list of _subjects_ (users, groups, or service accounts), and a reference to the role being granted. A RoleBinding grants permissions within a specific namespace whereas a ClusterRoleBinding grants that access cluster-wide.

A RoleBinding may reference any Role in the same namespace. Alternatively, a RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding. If you want to bind a ClusterRole to all the namespaces in your cluster, you use a ClusterRoleBinding.

#### **RoleBinding In DIGIT**[ ](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-example)

Here is the Digit [rolebinading](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/helm/charts/cluster-configs/templates/rbac/rolebindings.yaml) that we are using to grant access to group

{% code lineNumbers="true" %}
```
{{- with index .Values "cluster-configs" "rbac" }}
{{- range $idx, $v := . }}                 // These iteration values are defined in the environment file
{{- range $nsidx, $nsval := .namespaces }}  // These iteration values are defined in the environment file 
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: digit-{{ $v.role }}
  namespace: {{ $nsval }}
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: digit-{{ $v.role }}
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: Group
  name: digit-user        
---
{{- end }}
{{- end }}
{{- end }}
```
{% endcode %}

A RoleBinding can also reference a ClusterRole to grant the permissions defined in that ClusterRole to resources inside the RoleBinding's namespace. This kind of reference lets you define a set of common roles across your cluster, and then reuse them within multiple namespaces.

For instance, even though the following RoleBinding refers to a ClusterRole, "dave" (the subject, case sensitive) will only be able to read Secrets in the "development" namespace, because the RoleBinding's namespace (in its metadata) is "development".

#### Define the RBAC config in the Environment file

You must add a namespace to a role section to grant access to a group of a namespace.

{% code lineNumbers="true" %}
```
cluster-configs:
  rbac:
    - role: user
      namespaces: [egov] // digit-user ClusterRole would be granted to the playground and egov namespace. 
    - role: admin
      namespaces: [playground,egov]  // digit-admin ClusterRole would be granted to the playground and egov namespace. 
```
{% endcode %}

