FROM centos:7.5.1804
MAINTAINER pader "henry.box@outlook.com"

# set environment
ENV BASE_DIR="/home/sentinel" \
    JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk" \
    JAVA="/usr/lib/jvm/java-1.8.0-openjdk/bin/java" \
    JVM_XMS="1g" \
    JVM_XMX="1g" \
    JVM_XMN="512m" \
    JVM_MS="128m" \
    JVM_MMS="320m" \
    TIME_ZONE="Asia/Shanghai"

ARG VERSION=0.0.0
ARG HOT_FIX_FLAG=""

WORKDIR $BASE_DIR

RUN set -x \
    && yum update -y \
    && yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel wget iputils nc  vim libcurl
RUN wget  https://github.com/alibaba/Sentinel/releases/download/${VERSION}${HOT_FIX_FLAG}/sentinel-dashboard-${VERSION}.jar -P $BASE_DIR
RUN yum autoremove -y wget \
    && ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone \
    && yum clean all

EXPOSE 8080

CMD java \
    -Dserver.port=8080 \
    -Dcsp.sentinel.dashboard.server=localhost:8080 \
    -Dproject.name=sentinel-dashboard \
    -jar sentinel-dashboard.jar
