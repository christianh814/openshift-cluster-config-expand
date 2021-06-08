# Openshift Cluster Config Expanded
Setting up an OpenShift cluster using Kustomize and ArgoCD by using [openshift-cluster-config](https://github.com/christianh814/openshift-cluster-config) as a base

This is to show you can load in core components from one repo and use `kustomize` to modify it/add to it for your specifc cluster with anotherin a GitOps method of managing clusters.

This repo sets up OpenShift with Day 2 thingys via Argo CD. It also uses Dex (unsupported) for Authentication with OpenShift.

## Installing ArgoCD

Install Argo CD via the Operator Hub as described in the [cluster config repo](https://github.com/christianh814/openshift-cluster-config#installing-argocd)

## Deploying this Repo

To configure your cluster to this repo run

```
oc apply -k https://github.com/christianh814/openshift-cluster-config-expand/cluster-config/config/overlays/default
```

This will configure your server with the following.

Everything Mentioned in the [OpenShift Cluster Config repo](https://github.com/christianh814/openshift-cluster-config#deploying-this-repo) is [included in this repo](cluster-config/config/overlays/default/kustomization.yaml#L7) (as to not duplicate YAML).

This repo adds the additional settings/configs/apps...

* Deploying the EFK stack via OLM
  * Assumes you have [big enough](https://docs.openshift.com/container-platform/latest/logging/cluster-logging-deploying.html#cluster-logging-deploy-console_cluster-logging-deploying) workers
  * Assumes you're on AWS using [`gp2`](manifests/efk/install/clo-instance.yaml#L3) as your `storageClass`
* Deploys an app called BGD into the `bgd` namespace
  * The `marketing` group has `edit` access to this namespace
* ArgoCD
  * The `marketing` group can sync the `bgdk-green-app` application in the `bgdk` project.

## Making Changes

Either a PR to this repo or the [OpenShift Cluster Config repo](https://github.com/christianh814/openshift-cluster-config)...it's GitOps!
