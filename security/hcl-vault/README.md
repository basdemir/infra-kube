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

helm upgrade --install vault hashicorp/vault  --set='server.ha.enabled=true' --set='server.ha.raft.enabled=true' --set='injector.enabled=false' --set='csi.enabled=true' --version 0.13.0

helm upgrade --install --create-namespace --namespace vault vault hashicorp/vault \
  --set 'server.ha.enabled=true' \
	--set 'server.ha.raft.enabled=true' \
	--set 'injector.enabled=false' \
	--set 'csi.enabled=true'


helm install vault hashicorp/vault \
  --set 'server.ha.enabled=true' \
  --set 'server.ha.raft.enabled=true'

```

Unseal Key 1: I0Dw+oynfb18EqrklE3GvhYlTT6OmltFe9CAJ/D/5S/0
Unseal Key 2: lSWMCBGK9XBbmem7w3Wv/7V/FI1W37L8OR075f2VzK75
Unseal Key 3: Dba3IJd06aic+SLQrDRB7Iwd+WkpARrpyJUDBRI0k65H
Unseal Key 4: zdr0f+uxK9lnGU/FVUwcowiIpaTYOsEL/mrsKJ1TRcuR
Unseal Key 5: ir51Ty88gMKGquUPk8z14P74G7/wymp0q/UuBh+fnEyo

Initial Root Token: s.9RNrr18ZKrmQqBaVzdyxNYzX

