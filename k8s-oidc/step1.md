Deployment configuration for Keycloak instance :


<pre class="file" data-filename="kc-deploy.yaml" data-target="replace">apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
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
</pre>


Service configuration for Keycloak instance :

<pre class="file" data-filename="kc-service.yaml" data-target="replace">kind: Service
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
</pre>

Then deploy your app :

`kubectl apply -f kc-deploy.yaml`{{execute}}
`kubectl apply -f kc-service.yaml`{{execute}}



`
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
`{{execute}}
