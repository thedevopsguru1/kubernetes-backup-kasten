# kubernetes-backup-kasten
## Install Kasten helm chart
```
helm repo add kasten https://charts.kasten.io/
```
```
helm repo update
```
### Without the Cert manager
```
  helm upgrade --install my-kasten kasten/k10 --namespace kasten-io --create-namespace --set ingress.host="backup.anaeleboo.com" --set ingress.tls.enabled=true  --set ingress.tls.secretName="kasten" --set ingress.create=true --set auth.basicAuth.enabled=true --set auth.basicAuth.htpasswd='admin:$apr1$n9lqwrmo$idVPyIMQRP15TQJs.XO/A0' --set ingress.class=nginx
```
### To use the cert use , Install it using 
```
helm upgrade --install my-kasten kasten/k10 --namespace kasten-io --create-namespace  --set ingress.create=true --set auth.basicAuth.enabled=true --set auth.basicAuth.htpasswd='admin:$apr1$n9lqwrmo$idVPyIMQRP15TQJs.XO/A0'
```
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-new-ingress2
  annotations:
    kubernetes.io/ingress.class: "nginx"
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
spec:
  tls:
  - hosts:
    - backup.anaeleboo.com
    secretName: example-tls
  rules:
  - host: backup.anaeleboo.com
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: gateway
            port:
              number: 8000
 
```
#### Use this url
```
backup.anaeleboo.com/my-kasten/
```
