# Overview

Provides a set of kubernetes adminstrative access, contorl, and visibility tooling.

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

