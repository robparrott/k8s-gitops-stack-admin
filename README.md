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

```
kubectl port-forward service/kubernetes-dashboard -n kube-system 8443:443 
```

Then access at 

* https://localhost:8443

## WeaveScope

Port-forward:

```
kubectl port-forward service/weave-scope-app -n weave 9080:80 
```

Then access at 

* https://localhost:9080

