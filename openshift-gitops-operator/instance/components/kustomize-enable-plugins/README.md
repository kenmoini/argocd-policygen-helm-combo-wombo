# kustomize-build-policy-generator

## Purpose
This component is designed to turn on the `--enable-helm` and `--enable-alpha-plugins` feature of `kustomize build` in ArgoCD to support Helm Charts and PolicyGenerators inside of a kustomization.yaml file.

To learn more about the `--enable-helm` feature, refer to the ArgoCD docs [here](https://argo-cd.readthedocs.io/en/stable/user-guide/kustomize/#kustomizing-helm-charts) or the kustomize [examples](https://github.com/kubernetes-sigs/kustomize/blob/master/examples/chart.md).

## Usage

This component can be added to a base by adding the `components` section to your overlay `kustomization.yaml` file:

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - ../../base

components:
  - ../../components/kustomize-enable-plugins
```
