## Kubelilin依赖Jenkins插件列表：
* Kubernetes
* Pipeline
* Blue Ocean
* HTTP Request Plugin

## Jenkins for Docker 构建与部署
```sh
$ docker build . -t kubelilin/jenkins:v2.361.3-lts-alpine

$ docker run \
  --name jenkins-server \
  -d \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins-data:/var/jenkins_home \
  kubelilin/jenkins:v2.361.3-lts-alpine
  
$ docker exec -it jenkins-server /bin/bash
jenkins@93f88d6ca212:/$ cat /var/jenkins_home/secrets/initialAdminPassword

显示密码
```

## 获取已有实例插件列表
```sh
JENKINS_HOST=username:password@myhost.com:port
curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/'
```

## 构建镜像安装插件
从上述方法中获取到已安装的插件列表更新到plugins.txt文件中，构建时会自动安装。
```sh
docker build . -t kubelilin/jenkins:v2.361.3-lts-alpine
```

## 目前已集成的插件列表
```
git:4.11.5
workflow-scm-step:400.v6b_89a_1317c9a_
workflow-cps:2660.2664.v4c114e93f4c1
kubernetes:3651.v908e7db_10d06
ace-editor:1.1
jdk-tool:55.v1b_32b_6ca_f9ca
metrics:4.1.6.1-358.vf46b_95ea_d2b_3
blueocean-github-pipeline:1.25.8
pipeline-graph-analysis:195.v5812d95a_a_2f9
cloudbees-folder:6.740.ve4f4ffa_dea_54
momentjs:1.1.1
htmlpublisher:1.31
trilead-api:1.67.vc3938a_35172f
mina-sshd-api-core:2.9.1-44.v476733c11f82
bootstrap5-api:5.2.0-1
matrix-project:772.v494f19991984
jackson2-api:2.13.4.20221013-295.v8e29ea_354141
snakeyaml-api:1.31-84.ve43da_fb_49d0b
pubsub-light:1.16
blueocean-rest-impl:1.25.8
token-macro:308.v4f2b_ed62b_b_16
credentials:1087.1089.v2f1b_9a_b_040e4
jaxb:2.3.6-1
pipeline-stage-step:293.v200037eefcd5
blueocean-autofavorite:1.2.5
okhttp-api:4.9.3-108.v0feda04578cf
workflow-basic-steps:2.24
blueocean-config:1.25.8
caffeine-api:2.9.3-65.v6a_47d0f4d1fe
favorite:2.4.1
authentication-tokens:1.4
pipeline-model-api:2.2064.v5eef7d0982b_e
handy-uri-templates-2-api:2.1.8-22.v77d5b_75e6953
pipeline-build-step:2.18
pipeline-milestone-step:101.vd572fef9d926
lockable-resources:2.18
workflow-cps-global-lib:588.v576c103a_ff86
blueocean-git-pipeline:1.25.8
sshd:3.242.va_db_9da_b_26a_c3
blueocean:1.25.8
handlebars:3.0.8
command-launcher:81.v9c2cb_cb_db_392
blueocean-core-js:1.25.8
echarts-api:5.3.3-1
plugin-util-api:2.17.0
blueocean-pipeline-editor:1.25.8
pipeline-rest-api:2.27
credentials-binding:523.vd859a_4b_122e6
blueocean-web:1.25.8
blueocean-pipeline-api-impl:1.25.8
ssh-credentials:277.280.v1e86b_7d0056b_
matrix-auth:3.1.5
pipeline-stage-tags-metadata:2.2064.v5eef7d0982b_e
bouncycastle-api:2.26
popper2-api:2.11.6-1
jenkins-design-language:1.25.8
jquery-detached:1.2.1
windows-slaves:1.8.1
mailer:414.vcc4c33714601
durable-task:501.ve5d4fc08b0be
junit:1.59
blueocean-jwt:1.25.8
apache-httpcomponents-client-4-api:4.5.13-138.v4e7d9a_7b_a_e61
github-api:1.303-400.v35c2d8258028
jsch:0.1.55.61.va_e9ee26616e7
antisamy-markup-formatter:2.7
jjwt-api:0.11.5-77.v646c772fddb_0
workflow-support:815.vd60466279fc8
cloudbees-bitbucket-branch-source:784.v7fcdc7c670f6
pipeline-stage-view:2.27
pipeline-input-step:456.vd8a_957db_5b_e9
checks-api:1.7.5
jquery3-api:3.6.1-1
display-url-api:2.3.5
font-awesome-api:6.1.2-1
popper-api:1.16.1-3
sse-gateway:1.25
workflow-step-api:639.v6eca_cd8c04a_a_
javax-mail-api:1.6.2-6
variant:59.vf075fe829ccb
greenballs:9.13
git-server:1.11
mina-sshd-api-common:2.9.1-44.v476733c11f82
pipeline-model-definition:2.2064.v5eef7d0982b_e
structs:324.va_f5d6774f3a_d
kubernetes-client-api:5.12.2-193.v26a_6078f65a_9
javax-activation-api:1.2.0-3
workflow-multibranch:716.vc692a_e52371b_
github-branch-source:1637.vd833b_7ca_7654
pipeline-groovy-lib:612.v84da_9c54906d
blueocean-pipeline-scm-api:1.25.8
git-client:3.11.2
branch-api:2.1046.v0ca_37783ecc5
scm-api:621.vda_a_b_055e58f7
plain-credentials:139.ved2b_9cf7587b
blueocean-events:1.25.8
blueocean-dashboard:1.25.8
http_request:1.16
workflow-api:1153.vb_912c0e47fb_a_
script-security:1138.v8e727069a_025
blueocean-rest:1.25.8
workflow-durable-task-step:1139.v252a_e12e8463
blueocean-display-url:2.4.1
workflow-job:1174.1176.va_29023983d67
workflow-aggregator:590.v6a_d052e5a_a_b_5
pipeline-model-extensions:2.2064.v5eef7d0982b_e
kubernetes-credentials:0.9.0
blueocean-i18n:1.25.8
blueocean-personalization:1.25.8
blueocean-bitbucket-pipeline:1.25.8
bootstrap4-api:4.6.0-5
github:1.34.3.1
blueocean-commons:1.25.8
```
