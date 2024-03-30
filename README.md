Vanilla OKD Console integration with Keycloak OIDC

## Software version:

```Keycloak: 23.0.7```


```Kubernetes: 1.26.5```


```OpenShift console: 4.12 or 4.13```



**Run Keycloak on port 443 with custom domain or setup as systemd service**

1) ```bash kc.sh start-dev --https-certificate-file=/etc/letsencrypt/live/auth.dev-ops.kz/fullchain.pem --https-certificate-key-file=/etc/letsencrypt/live/auth.dev-ops.kz/privkey.pem --https-port=443```

2) create client with these settings
![image](https://github.com/Nurlan199206/okd-console-oidc/assets/22808731/feaf845d-48d7-4f23-a9d6-368754c7e123)


3) Create scopes for OIDC client ```openid``` ```groups``` ```email``` ```profile```
![image](https://github.com/Nurlan199206/okd-console-oidc/assets/22808731/2f75b7e0-c825-4ed8-87f3-466910642167)





**Add to each master node OIDC settings in ```/etc/kubernetes/manifests/kube-apiserver.yaml```**
```
- --oidc-issuer-url=https://auth.dev-ops.kz/realms/kubernetes
- --oidc-client-id=kubernetes
- --oidc-groups-claim=groups
- --oidc-username-claim=preferred_username
```

4) create user 
![image](https://github.com/Nurlan199206/okd-console-oidc/assets/22808731/83ffa46a-83a7-4e65-8c0c-6c03a21ab96c)


5) ```kubectl create clusterrolebinding admin --clusterrole=cluster-admin --user https://auth.dev-ops.kz/realms/kubernetes#admin```
 


https://github.com/Nurlan199206/okd-console-oidc/assets/22808731/b01d906f-231b-4fac-8bfd-c69fe9e0651b

