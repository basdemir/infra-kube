# ARGOCD 

## Installation

```bash
 kustomize build deploy/overlays/dev | kubectl apply -f - # or
 kubectl apply -k deploy/overlays/dev/
 ## Get secret
 kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

 kubectl -n argocd port-forward service/argocd-server 8080:80
 ```