```bash
# download latest release of istio
curl -L https://istio.io/downloadIstio | sh -
sudo cp istio-1.10.3/bin/istioctl /usr/local/bin

istioctl operator init --hub dockerepo.hvl.io/tools/istio

istioctl profile dump default > profile-default.yaml
istioctl install --filename profile-default.yaml

# Demo App

kubectl create namespace bookinfo
kubectl label namespace bookinfo istio-injection=enabled

kubectl get ns bookinfo --show-labels

export ISTIO_REL_DIR=~/istio-1.10.3

ka ${ISTIO_REL_DIR}/samples/bookinfo/platform/kube/bookinfo.yaml
ka ${ISTIO_REL_DIR}/samples/bookinfo/networking/bookinfo-gateway.yaml

export GATEWAY_URL=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].ip}') # dns var ise .hostname 

echo "http://${GATEWAY_URL}/productpage"


cat <<EOF > patch.yaml
spec:
  template:
    spec:
      dnsPolicy: ClusterFirst
      imagePullSecrets:
      - name: dockerhub
EOF

# kubectl patch deployment details-v1 --patch "$(cat patch.yaml)"

deps=$(kubectl get deployments -n bookinfo | awk '{if (NR!=1)  {print $1}}' | xargs echo)

kubectl patch deployment $(echo $deps) --patch "$(cat patch.yaml)"

# Delete
namespace=istio-system
kubectl delete namespace $namespace

cat <<EOF | curl -k -X PUT \
  127.0.0.1:8001/api/v1/namespaces/${namespace}/finalize \
  -H "Content-Type: application/json" \
  --data-binary @-
{
  "kind": "Namespace",
  "apiVersion": "v1",
  "metadata": {
    "name": "${namespace}"
  },
  "spec": {
    "finalizers": null
  }
}
EOF

kubectl get crd | grep --color=never 'istio.io' | awk '{print $1}' \
    | xargs -n1 kubectl delete crd

```


