you can import this application in intellij and run the application

**below are the instrumentation which enables the application to emmit the prometheus metrics**

`implementation 'org.springframework.boot:spring-boot-starter-actuator'
runtimeOnly 'io.micrometer:micrometer-registry-prometheus'`

Once the application is up and running you can access below URLs
[http://localhost:8080/actuator](All observability URI)
[http://localhost:8080/actuator/prometheus](Prometheus metrics endpoint)

Now let's bring prometehus in to the came, We are using Colima with docker for this setup.
`brew install colima
colima start
`
checkout the file [ext/prometheus.yaml](prometheus.yaml), at line No 20 change your ip address

In below change your 'APPLICATION_DIRECTORY'

`docker run -d --name=prometheus -p 9090:9090 \
    -v [APPLICATION_DIRECTORY]/ext/prometheus.yaml:/etc/prometheus/prometheus.yml prom/prometheus \
    --config.file=/etc/prometheus/prometheus.yml`

check [prometheus](http://localhost:9090/graph)



