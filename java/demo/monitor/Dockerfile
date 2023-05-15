FROM kubelilin/jdk:x86_64-alpine-ibm_semeru-8u345-b01_openj9-0.33.1


ADD ./app.jar .

ENTRYPOINT exec java -jar app.jar