FROM kubelilin/jdk:x86_64-alpine-eclipse-temurin-openjdk1704


ADD ./target/app.jar .

ENTRYPOINT exec java -jar app.jar