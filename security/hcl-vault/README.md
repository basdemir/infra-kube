# HCL Vault on Kubernetes

```bash
cat << EOF > ./override-values.yml
server:
  ha:
    enabled: true
    replicas: 5

EOF
```


```bash
https://www.vaultproject.io/docs/platform/k8s/helm/examples/ha-with-raft

helm install vault hashicorp/vault \
  --set='server.ha.enabled=true' \             
  --set='server.ha.raft.enabled=true'
```