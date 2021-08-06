```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```
```bash
helm upgrade --install prometheus --version=17.1.1 --namespace monitoring --create-namespace -f /home/dev/projects/Kubernetes/k8stools/prometheus/prometheus-default-values-17.1.1.yaml prometheus-community/kube-prometheus-stack
```
