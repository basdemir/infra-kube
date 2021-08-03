# K3S - Lightweigth K8s

## Download `k3sup` (tl;dr)

`k3sup` is distributed as a static Go binary. You can use the installer on MacOS and Linux, or visit the [Releases page](https://github.com/alexellis/k3sup/releases) to download the executable for Windows.

```sh
curl -sLS https://get.k3sup.dev | sh
sudo install k3sup /usr/local/bin/

k3sup --help

k3sup install --host k3s.ecospend.io --user <username> --ssh-key ~/.ssh/<user priv key> # or

k3sup install --host k3s.ecospend.io --user <username> --ssh-key ~/.ssh/<user priv key> --k3s-extra-args '--no-deploy traefik'
```
