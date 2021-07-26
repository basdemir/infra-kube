## install with changed values

helm upgrade --install grafana grafana/grafana -f grafana-my-values.yaml -n grafana --create-namespace

## admin password

kubectl get secret --namespace grafana grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

KEY_FILE=grafana.key
CERT_FILE=grafana.crt
HOST=poc.adzuki.io
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ${KEY_FILE} -out ${CERT_FILE} -subj "/CN=${HOST}/O=${HOST}"
