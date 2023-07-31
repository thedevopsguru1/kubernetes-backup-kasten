# kubernetes-backup-kasten
## Install Kasten helm chart
```
helm repo add kasten https://charts.kasten.io/
```
```
helm repo update
```
```
 helm upgrade --install my-kasten kasten/k10 --namespace kasten-io --create-namespace --set ingress.host="backup.anaeleboo.com" --set ingress.tls.enabled=true  --set ingress.tls.secretName="kasten" --set ingress.create=true --set auth.basicAuth.enabled=true --set auth.basicAuth.htpasswd='admin:$apr1$n9lqwrmo$idVPyIMQRP15TQJs.XO/A0' --set ingress.class=nginx
```
##### Need to setup Cert
