# Install keycloak

``` yaml
cat <<EOF | kubectl create -f -
apiVersion: apps/v1beta2 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: keycloak-deployment
  labels:
    app: keycloak
spec:
  replicas: 1
  selector:
    matchLabels:
      app: keycloak
  template:
    metadata:
      labels:
        app: keycloak
    spec:
      containers:
      - name: keycloak
        image: jboss/keycloak
        ports:
        - containerPort: 8080
---
kind: Service
apiVersion: v1
metadata:
  name: keycloak-service
spec:
  selector:
    app: keycloak
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
  type: LoadBalancer
---
EOF
```

# Create realm and Configure

* In keycloak create realm kubernetes
* Create a client Kubernetes



# Configure API server

https://kubernetes.io/docs/admin/authentication/#option-1---oidc-authenticator

``` bash
vi /etc/kubernetes/manifests/kube-apiserver.yaml

# add parameters
  - --oidc-issuer-url keycloak-url.domain
  # OIDC keycloak client (kubernetes)
  - --oidc-client-id kubernetes
  # username for AD federation (no emails in INTRA-DEV)
  - --oidc-username-claim username
  # need to give the CA used for keycloak
  - --oidc-ca-file
```
