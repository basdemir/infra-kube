## Installation

Run `Following:`

```
git clone https://github.com/kubernetes-sigs/sig-storage-local-static-provisioner.git
cd sig-storage-local-static-provisioner

ka deployment/kubernetes/example/default_example_storageclass.yaml

kubectl patch storageclass fast-disks -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-def
ault-class":"true"}}}'

helm template ./helm/provisioner > deployment/kubernetes/provisioner_generated.yaml

ka deployment/kubernetes/provisioner_generated.yaml # or

kustomize build deployment/kubernetes | kubectl apply -f - # or

kubectl apply -k deployment/kubernetes
```
