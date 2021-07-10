k -n cert-manager-self create deployment nginx --image dockerepo.hvl.io/rancher/nginx:1.17.4-alpine
k -n cert-manager-self expose deployment nginx --port 80 
