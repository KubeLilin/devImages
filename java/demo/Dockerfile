FROM kubelilin/jdk:x86_64-alpine-eclipse-temurin-openjdk1704

WORKDIR /data

ADD ./app.jar .
ADD ./jmx_prometheus_javaagent-0.18.0.jar .
ADD ./config.yaml .

ENTRYPOINT exec java -javaagent:./jmx_prometheus_javaagent-0.18.0.jar=12345:config.yaml  -jar app.jar --server.port=8080
