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
```
