# Openshift Cluster Config Expanded
Setting up an OpenShift cluster using Kustomize and ArgoCD by using [openshift-cluster-config](https://github.com/christianh814/openshift-cluster-config) as a base

This is to show you can load in core components from one repo and use `kustomize` to modify it/add to it for your specifc cluster with anotherin a GitOps method of managing clusters.


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

## Deploying this Repo

To configure your cluster to this repo run

```
oc apply -k https://github.com/christianh814/openshift-cluster-config-expand/cluster-config/config/overlays/default
```

This will configure your server with the following.

Everything Mentioned in the [OpenShift Cluster Config repo](https://github.com/christianh814/openshift-cluster-config#deploying-this-repo)

Additionally...

* Deploying the EFK stack via OLM
  * Assumes you have [big enough](https://docs.openshift.com/container-platform/latest/logging/cluster-logging-deploying.html#cluster-logging-deploy-console_cluster-logging-deploying) workers
  * Assumes you're on vCenter using [`thin`](manifests/efk/install/clo-instance.yaml#L3) as your `storageClass`
* Deploys an app called BGD into the `bgd` namespace
  * The `marketing` group has `edit` access to this namespace
* ArgoCD
  * The `marketing` group can sync the `bgdk-green-app` application in the `bgdk` project.

## Making Changes

Either a PR to this repo or the [OpenShift Cluster Config repo](https://github.com/christianh814/openshift-cluster-config)...it's GitOps!
