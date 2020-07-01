# Openshift Cluster Config Expanded
Setting up an OpenShift cluster using Kustomize and ArgoCD by using [openshift-cluster-config](https://github.com/christianh814/openshift-cluster-config) as a base

This is to show you can load in core components and use `kustomize` to modify it/add to it for your specifc cluster.


## Installing ArgoCD

> :warning: This is based on the argocd operator v0.9 using an "Automatic" update strategy ...[Andrew](https://github.com/pittar) says there's breaking changes coming in v0.10 - so be warned!

To install argocd using the operator, use the [openshift-cluster-config repo](https://github.com/christianh814/openshift-cluster-config#installing-argocd)

```
oc apply -k https://github.com/christianh814/openshift-cluster-config/argocd/install
```

__NOTE__

You may get an error that looks like this...

```
no matches for kind "ArgoCD" in version "argoproj.io/v1alpha1"
```

That's okay, just run the `oc apply -k` command again.

