FROM adoptopenjdk/openjdk8-openj9:x86_64-alpine-jdk8u345-b01_openj9-0.33.1

ENV LANG=C.UTF-8 \
    TZ="Asia/Shanghai" \
    TINI_VERSION="v0.19.0"

# Install base packages
RUN apk add --no-cache tini \
#   freetype-dev \  
    --update ttf-dejavu fontconfig \ 
     && rm -rf /var/cache/apk/*

# Install skyworking agent
WORKDIR /data/skyagent/agent/agent
COPY ./agent /data/skyagent/agent/agent

WORKDIR /data/prometheus

# Install promethus agent
COPY ./jmx_prometheus_javaagent-0.17.2.jar ./jmx_prometheus_javaagent.jar
COPY ./config.yaml ./

WORKDIR /data/arthas
RUN wget https://arthas.gitee.io/arthas-boot.jar

ENTRYPOINT ["tini", "--"]