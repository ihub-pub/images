FROM openjdk:8u201-jdk-alpine3.9

# set environment
ENV BASE_DIR="/home/sentinel" \
    JVM_XMS="1g" \
    JVM_XMX="1g" \
    JVM_XMN="512m" \
    JVM_MS="128m" \
    JVM_MMS="320m" \
    TIME_ZONE="Asia/Shanghai"

ARG VERSION=0.0.0

WORKDIR $BASE_DIR

RUN wget  https://github.com/alibaba/Sentinel/releases/download/${VERSION}/sentinel-dashboard-${VERSION}.jar -P $BASE_DIR

EXPOSE 8080

CMD java \
    -Dserver.port=8080 \
    -Dcsp.sentinel.dashboard.server=localhost:8080 \
    -Dproject.name=sentinel-dashboard \
    -jar sentinel-dashboard*.jar
