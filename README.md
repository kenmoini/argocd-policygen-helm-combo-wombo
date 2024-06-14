# ArgoCD + PolicyGenerator + Helm Combo Wombo

> An example in how to get ArgoCD working with PolicyGenerators and Helm for the ultimate in templating fun.  Oh an an AppSet example too.

## Setup

1. Install the OpenShift GitOps Operator: `oc apply -k openshift-gitops-operator/operator/overlays/latest/`
2. Configure OpenShift GitOps: `oc apply -k openshift-gitops-operator/instance/overlays/default/`
3. [Optional] Integrate RHACM and OpenShift GitOps: `oc apply -k rhacm-integration/`

## ApplicationSet Example

An ArgoCD ApplicationSet can be used to provide simple templating over a matrix of inputs such as available clusters managed by ArgoCD.

This repo has an example that will deploy the Hashicorp Vault via Helm to individual clusters using individual Helm Values for each cluster.

You can deploy this via `oc apply -k app-sets/hub/`

Once deployed, you can launch the ArgoCD dashboard and see individual Applications created from this AppSet prefixed with the managed cluster name.

Note that the targeting of this AppSet is done by labels on the managed clusters in ArgoCD - this by default relies on the RHACM integration that will automatically create ArgoCD clusters with all the labels that are managed in RHACM.

> Other Note: The Applications will not progress fully until the Vault pod is initialized:

```bash
oc exec -n vault local-cluster-vault-0 -- vault operator init
oc exec -n vault local-cluster-vault-0 -- vault operator unseal <unseal_key_1>
oc exec -n vault local-cluster-vault-0 -- vault operator unseal <unseal_key_2>
oc exec -n vault local-cluster-vault-0 -- vault operator unseal <unseal_key_3>
```