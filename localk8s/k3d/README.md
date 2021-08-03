# create k3d cluster

## k3d - no cpu config ??

```
curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash # or
brew install k3d

k3d cluster create devcluster \
--agents 3 --servers 3 \
--api-port 127.0.0.1:6443 \
-p 80:80@loadbalancer \
-p 443:443@loadbalancer \
--k3s-server-arg "--no-deploy=traefik"

k taint node k3d-devcluster2-server-0 node-role.kubernetes.io/master:NoSchedule

k3d cluster create devcluster \
--agents 2 --servers 1 \
--api-port 127.0.0.1:6443 \
-p 80:80@loadbalancer \
-p 443:443@loadbalancer \
--registry-config "$HOME/reg.yaml" \
--k3s-server-arg "--no-deploy=traefik"

#k3d reg.yaml

mirrors:
  docker.io:
    endpoint:
      - "https://registry.hub.docker.com"
        #      - "https://docker.io"
configs:
  "docker.io":
    auth:
      username: "b..s" # this is the registry username
      password: "1..D" # this is the registry password
```
## Exposing Services

https://k3d.io/usage/guides/exposing_services/

```bash
k3d cluster create devcluster \
--agents 2 --servers 1 \
--api-port 6550 \
-p 9080:80@loadbalancer \
-p 6443:443@loadbalancer \
--registry-config "$HOME/reg.yaml"

export KUBECONFIG="$(k3d kubeconfig write devcluster)"

kubectl create deployment nginx --image=nginx
kubectl create service clusterip nginx --tcp=80:80
# create nginx-ing.yaml
cat <<EOF | kubectl apply -f -
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx
  annotations:
    ingress.kubernetes.io/ssl-redirect: "false"
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx
            port:
              number: 80
EOF
# and apply

ka nginx-ing.yaml
curl localhost:9080/
```
<!-- ```bash
cat <<EOF | kubectl apply -f -
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: argocd
  annotations:
    # nginx.ingress.kubernetes.io/force-ssl-redirect: "true"
    # nginx.ingress.kubernetes.io/ssl-passthrough: "true"
    nginx.ingress.kubernetes.io/backend-protocol: "HTTP"
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: argocd-server
            port:
              number: 80
EOF

``` -->
