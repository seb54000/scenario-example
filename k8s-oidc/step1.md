The following snippet can be copied into the editor:

<pre class="file" data-filename="app.js" data-target="replace">apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
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
        - containerPort: 80
</pre>

Code can be executed with the syntax `node app.js`{{execute}}

The following will automatically be turned into a link and proxied to port 3000 -  http://[[CLIENT_SUBDOMAIN]]-3000-[[KATACODA_HOST]].environments.katacoda.com/

In a multi-host environment, such as Docker, use HOST_SUBDOMAIN instead of CLIENT_SUBDOMAIN.

Live example at https://www.katacoda.com/courses/nodejs/playground
