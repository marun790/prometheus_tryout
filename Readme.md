**This app is about setting up a spring boot app with prometheus**

you can import this application in intellij and run the application

**below are the instrumentation which enables the application to emmit the prometheus metrics**

`implementation 'org.springframework.boot:spring-boot-starter-actuator'`
`runtimeOnly 'io.micrometer:micrometer-registry-prometheus'`

Once the application is up and running you can access below URLs
[http://localhost:8080/actuator](All observability URI)
[http://localhost:8080/actuator/prometheus](Prometheus metrics endpoint)

Now let's bring prometehus in to the came, We are using Colima with docker for this setup.
`brew install colima`
`colima start`

checkout the file [ext/prometheus.yaml](prometheus.yaml), at line No 20 change your ip address

Now let's add node exporter for your machine

if you have brew you can install using below command

`brew install node_exporter`  

`brew services start node_exporter`


` - job_name: 'my_mac' ` in `[APPLICATION_DIRECTORY]/ext/prometheus.yaml` will help prometheus to scrape metrics of host machine which is your Mac


In below change your 'APPLICATION_DIRECTORY'

`docker run -d --name=prometheus -p 9090:9090 \
-v [APPLICATION_DIRECTORY]/ext/prometheus.yaml:/etc/prometheus/prometheus.yml prom/prometheus \
--config.file=/etc/prometheus/prometheus.yml`

check [prometheus](http://localhost:9090/graph) you should be able to view the prometheus UI and you can play with promql
