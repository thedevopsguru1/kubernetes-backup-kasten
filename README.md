# kubernetes-backup-kasten
## Install Kasten helm chart
```
helm repo add kasten https://charts.kasten.io/
```
```
helm repo update
```
```
 helm upgrade --install my-kasten kasten/k10 --namespace kasten-io --create-namespace  --set ingress.create=true --set auth.basicAuth.enabled=true --set auth.basicAuth.htpasswd='admin:$apr1$n9lqwrmo$idVPyIMQRP15TQJs.XO/A0' --set ingress.class=nginx --set ingress.annotations."nginx.ingress.kubernetes.io/ssl-redirect"="true" --set ingress.tls.enabled="true" --set ingress.host=kasten.anaeleboo.com
```
##### If you installed K10 with a different release name than k10 (specified via the --name option in the install command), the above URL should be modified to replace the last occurrence of k10 with the specified release name. The revised URL would look like http://127.0.0.1:8080/release-name-here/#/
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
### To generate the basicAuth username and password , use this : 
```
https://hostingcanada.org/htpasswd-generator/
```
