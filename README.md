# Overview

Provides a set of kubernetes adminstrative access, control, and visibility tooling.

The layout convention is as follows:

* `admin-stack.yaml`: provides a "stack" manifest definition for the entire set of packages
* `packages/`: path to a set of manifests which each provides a suite of functionality defined under `modules/`
* `modules/`: defines a single unit of deployment for an application on component; these may reference a path in implementation of a single helm chart
* `implementation/`: additional manifests pulled in to support a module.


# Accessing

Service Account "eks-admin" has a bearer token for access, so you need to dig that out to access Kubernetes Dashboard:

```
SECRET=$(kubectl -n kube-system get secret | grep eks-admin-token | awk '{print $1}')
TOKEN=$( kubectl -n kube-system describe secret ${SECRET} | grep "^token:" | awk '{print $2}' )
echo $TOKEN
```



## Kubernetes Dashboard:

For Kubernetes Dashboard access, use the kubernetes proxy command:
```
kubectl proxy
```

Then access at 

* http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:https/proxy/

Use the above token to connect.

## WeaveScope

Port-forward:

```
kubectl port-forward service/weave-scope-app -n weave 9080:80 
```

Then access at 

* https://localhost:9080

