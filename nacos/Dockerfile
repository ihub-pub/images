FROM amd64/buildpack-deps:buster-curl@sha256:c8aa318418d49b4d9865955785ed695ac8713243513a61590382ecb24536dbfa as installer

ARG VERSION=0.0.0

RUN set -x \
    && curl -SL --output /var/tmp/nacos-server.tar.gz https://github.com/alibaba/nacos/releases/download/${VERSION}/nacos-server-${VERSION}.tar.gz \
    && tar -xzvf /var/tmp/nacos-server.tar.gz -C /home \
    && rm -rf /var/tmp/nacos-server.tar.gz /home/nacos/bin/* /home/nacos/conf/*.properties /home/nacos/conf/*.example /home/nacos/conf/nacos-mysql.sql

FROM openjdk:11-jre-slim@sha256:93af7df2308c5141a751c4830e6b6c5717db102b3b31f012ea29d842dc4f2b02

# set environment
ENV MODE="cluster" \
    PREFER_HOST_MODE="ip"\
    BASE_DIR="/home/nacos" \
    CLASSPATH=".:/home/nacos/conf:$CLASSPATH" \
    CLUSTER_CONF="/home/nacos/conf/cluster.conf" \
    FUNCTION_MODE="all" \
    NACOS_USER="nacos" \
    JAVA="/usr/local/openjdk-8/bin/java" \
    JVM_XMS="1g" \
    JVM_XMX="1g" \
    JVM_XMN="512m" \
    JVM_MS="128m" \
    JVM_MMS="320m" \
    NACOS_DEBUG="n" \
    TOMCAT_ACCESSLOG_ENABLED="false" \
    TZ="Asia/Shanghai"

WORKDIR $BASE_DIR

# copy nacos bin
COPY --from=installer ["/home/nacos", "/home/nacos"]

ADD bin/docker-startup.sh bin/docker-startup.sh
ADD conf/application.properties conf/application.properties

# set startup log dir
RUN mkdir -p logs \
    && cd logs \
    && touch start.out \
    && ln -sf /dev/stdout start.out \
    && ln -sf /dev/stderr start.out
RUN chmod +x bin/docker-startup.sh

EXPOSE 8848
ENTRYPOINT ["bin/docker-startup.sh"]
