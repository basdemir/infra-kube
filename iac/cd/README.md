### Retrieve password of argo cd

```
kg secrets -n argocd argocd-initial-admin-secret -o json | jq -r .data.password | base64 -d && echo

kg secrets -n argocd argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d && echo
```
