Vanilla OKD Console integration with Keycloak OIDC

## Software version:

```Keycloak: 23.0.7```


```Kubernetes: 1.26.5```


```OKD Console image: 4.12```



**Run Keycloak on port 443 with custom domain**

1) ```bash kc.sh start-dev --https-certificate-file=/etc/letsencrypt/live/auth.dev-ops.kz/fullchain.pem --https-certificate-key-file=/etc/letsencrypt/live/auth.dev-ops.kz/privkey.pem --https-port=443```


**Add to each master node OIDC settings in /etc/kubernetes/manifests/kube-apiserver.yaml**
```
- --oidc-issuer-url=https://auth.dev-ops.kz/realms/kubernetes
- --oidc-client-id=kubernetes
- --oidc-groups-claim=groups
- --oidc-username-claim=preferred_username
```


10) ```kubectl create clusterrolebinding admin --clusterrole=cluster-admin --user https://auth.dev-ops.kz/realms/kubernetes#admin```
 
