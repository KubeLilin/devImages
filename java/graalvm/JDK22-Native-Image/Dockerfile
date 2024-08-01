# graalvm:mvn-jdk22
# docker build . -t graalvm:mvn-jdk22 -f Dockerfile_graalvm --no-cache
# docker run -it --rm --entrypoint /bin/bash graalvm:mvn-jdk22
# 镜像版本号来自 graalvm 官网 https://github.com/graalvm/container/pkgs/container/graalvm-ce
FROM ghcr.io/graalvm/jdk-community:22

ARG JDK_MAJOR_VERSION=22
ARG YUM_REPO=""
ARG YUM_REPO_DEFAULT=https://yum.oracle.com/repo/OracleLinux/OL9/graalvm/community/
ARG TEMP_REGION=""
ENV MAVEN_VERSION 3.9.6
ENV MAVEN_HOME /usr/lib/mvn
ENV PATH $MAVEN_HOME/bin:$PATH


RUN if [ "$YUM_REPO" == "" ]; then YUM_REPO_CURRENT="$YUM_REPO_DEFAULT\$basearch"; else YUM_REPO_CURRENT="$YUM_REPO"; fi \
    && echo -e "\
[ol9_graalvm_community]\n\
name=Oracle Linux 9 graalvm community (\$basearch)\n\
baseurl=$YUM_REPO_CURRENT\n\
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle\n\
gpgcheck=1\n\
enabled=1\
" > /etc/yum.repos.d/ol9_graalvm_community.repo \
    && echo "$TEMP_REGION" > /etc/dnf/vars/ociregion \
    && microdnf --enablerepo ol9_codeready_builder install -y graalvm-community-${JDK_MAJOR_VERSION}-native-image wget \
    && rm -rf /var/cache/yum \
    && echo "" > /etc/dnf/vars/ociregion \
    && echo -e "\
[ol9_graalvm_community]\n\
name=Oracle Linux 9 graalvm community (\$basearch)\n\
baseurl=$YUM_REPO_DEFAULT\$basearch\n\
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle\n\
gpgcheck=1\n\
enabled=1\
" > /etc/yum.repos.d/ol9_graalvm_community.repo

# RUN microdnf update -y oraclelinux-release-el9 \
#     && microdnf --enablerepo ol9_codeready_builder install -y graalvm-community-${JDK_MAJOR_VERSION}-native-image wget \
#     && microdnf clean all

RUN wget http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  tar -zxvf apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  rm apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  mv apache-maven-$MAVEN_VERSION /usr/lib/mvn



# 外部使用
#   docker run --rm -it \
#         -v $PWD:/mnt/myproject:rw \
#         -w /mnt/myproject \
#         graalvm:mvn-jdk22 \
#         mvn clean -Pnative native:compile
