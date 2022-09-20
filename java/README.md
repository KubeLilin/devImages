
# 基于Alpine构建,支持 JDK 8 & JDK 17.

# 集成
* Skyworking Agent 8.12.0
* Promethus Agent 0.17.2
* Arthas

# 构建JDK8
```bash
docker build . -t kubelilin/jdk:x86_64-alpine-jdk8u345-b01_openj9-0.33.1 --platform=amd64
```

# 构建JDK17
```bash
docker build -f ./Dockerfile_JDK1704 -t kubelilin/jdk:x86_64-alpine-eclipse-temurin-openjdk1704 . --platform=amd64
```

```bash
docker build -f ./Dockerfile_SemeruJDK8 -t kubelilin/jdk:x86_64-alpine-ibm_semeru-8u345-b01_openj9-0.33.1 . --platform=amd64

docker build . -t kubelilin/jdk:x86_64-alpine-ibm_semeru-jdk17041_openj9-0.33.1 --platform linux/x86_64 --no-cache
```

# 镜像使用 例jdk1.8
```dockerfile
FROM kubelilin/jdk:x86_64-alpine-jdk8u345-b01_openj9-0.33.1
WORKDIR /data
# 将代码复制到容器中
ADD target/app.jar .
ENV JAVA_OPTS=""
ENV PROMETHEUS_OPS="-javaagent:/data/prometheus/jmx_prometheus_javaagent.jar=12345:/data/prometheus/config.yaml"
# 启动容器时运行的命令
ENTRYPOINT exec java  -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -Dfile.encoding=UTF-8 -Djava.security.egd=file:/dev/./urandom -XX:MaxRAMPercentage=80.0 $JAVA_OPTS -javaagent:/data/skyagent/agent/skywalking-agent.jar -Dskywalking.agent.service_name=chehou-paycenter-chargetask -Dskywalking.collector.backend_service=127.0.0.1:11800,127.0.0.1:11800 -javaagent:/data/prometheus/jmx_prometheus_javaagent.jar=12345:/data/prometheus/config.yaml -jar /data/app.jar $SPRING_OPTS
```