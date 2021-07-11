# Tools for Kubernetes Clusters

## Logging

---

### Grafana Loki Stack

---

[Grafana Loki Stack URL](https://grafana.com/docs/loki/latest/installation/helm/)

```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

## create loki-stack-values.yaml with

helm show values grafana/loki-stack > loki-stack-values.yaml
helm upgrade --install loki grafana/loki-stack -f loki-stack-values.yaml -n logging --create-namespace

## to pathc the tolerations cerate a patch file and run:

kubectl patch daemonsets.apps loki-promtail --patch "$(cat patch-tolerations.yaml)"
kubectl patch statefulsets.apps loki --patch "$(cat patch-tolerations.yaml)"

kubectl port-forward service/loki-grafana 3000:80

# username: admin password is:

kubectl get secret --namespace logging loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
