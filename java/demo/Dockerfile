# FROM kubelilin/jdk:x86_64-alpine-eclipse-temurin-openjdk1704
# FROM kubelilin/jdk:x86_64-alpine-ibm_semeru-8u345-b01_openj9-0.33.1
# FROM kubelilin/jdk:x86_64-alpine-ibm_semeru-jdk17041_openj9-0.33.1
FROM kubelilin/jdk:x86_64-alpine-ibm_semeru-8u345-b01_openj9-0.33.1

WORKDIR /data

ADD ./app.jar .

ENTRYPOINT exec java -jar app.jar