FROM kubelilin/jdk:x86-graalvm-mvn-jdk22 AS builder

WORKDIR /publish
COPY . .
RUN mvn clean -DskipTests -Pnative native:compile

# 最终容器, 基础镜像alpine 中包含 tini
FROM kubelilin/alpine:3.20.2-x86-graalvm-native AS production

COPY --from=builder /publish/target/demo1 /application/app

WORKDIR /application
CMD ["./app"]
