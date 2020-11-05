# Namespace Separate Envs

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

Blog Post: [Kustomize vs Helm vs Kubes: Kubernetes Deploy Tools](https://blog.boltops.com/2020/11/05/kustomize-vs-helm-vs-kubes-kubernetes-deploy-tools)

Simple example with namespace to separate environments like dev and prod.

## Structure

    ├── Chart.yaml
    ├── README.md
    ├── templates
    │   ├── deployment.yaml
    │   ├── _helpers.tpl
    │   ├── NOTES.txt
    │   ├── serviceaccount.yaml
    │   └── service.yaml
    └── values.yaml

One interesting note about how helm works with namespaces is that the `--namespace` option, helm switches to the namespace to creates the resources. So the namespace field does not have to be set in the YAML files themselves.

## Create Different Environments

dev:

    $ helm install chart-dev . --namespace chart-dev --create-namespace -f values/dev.yaml
    $ k get deploy -n chart-dev
    NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/chart-dev-demo   1/1     1            1           20s

prod:

    $ helm install chart-prod . --namespace chart-prod --create-namespace -f values/dev.yaml
    $ k get deploy -n chart-prod
    NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/chart-prod-demo   1/1     1            1           20s

## Cleanup

    $ helm uninstall chart-dev
    $ k delete ns chart-dev # cleanup namespace
    $ helm uninstall chart-prod
    $ k delete ns chart-prod # cleanup namespace

