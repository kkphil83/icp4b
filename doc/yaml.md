

# Deployment Strategies on Kubernetes

![](img/2019-11-05-17-46-41.png)


## Ingress

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: samstore-ing
spec:
  rules:
  - host: petstore.icp4a.com
    http:
      paths:
      - path: /
        backend:
          serviceName: samstore-svc
          servicePort: 80
```


## Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: samstore-svc
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: tomcat
  selector:
    app: samstore-pod
```


## ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: datasource
data:
  application.properties: |-
    # Oracle settings-CLI
    spring.datasource.url=jdbc:oracle:thin:@//techdns.iptime.org:24001/xe
    spring.datasource.username=oracle
    spring.datasource.password=oracle
    # spring.datasource.driver-class-name=oracle.jdbc.driver.OracleDriver
    spring.datasource.driver-class-name=oracle.jdbc.OracleDriver
    spring.jpa.database-platform=org.hibernate.dialect.Oracle10gDialect
    # HikariCP settings
    # spring.datasource.hikari.*
    mybatis.mapper-locations=mybatis/**/*.xml
    server.port=9090
    environment.data.path=classpath:data.json
    #logging configuraion
    logging.config=classpath:logback.xml
    spring.datasource.hikari.connection-timeout=60000
    spring.datasource.hikari.maximum-pool-size=5
```


## Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: samstore-deploy
  labels:
    app: samstore-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: samstore-pod
  strategy:
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: samstore-pod
    spec:
      containers:
      - name: samstore
        image: myguddy/samstore
        ports:
        - containerPort: 9090
          name: tomcat
        imagePullPolicy: Always
        resources:
          limits:
            cpu: 500m
            memory: 1024Mi
          requests:
            cpu: 300m
            memory: 256Mi
        volumeMounts:
        - name: application-property
          mountPath: /config
      volumes:
      - name: application-property
        configMap:
        # Provide the name of the ConfigMap containing the files you want
        # to add to the container
          name: datasource
```


