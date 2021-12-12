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
ARG PORT=8080

WORKDIR $BASE_DIR

RUN wget  https://github.com/alibaba/Sentinel/releases/download/${VERSION}/sentinel-dashboard-${VERSION}.jar -P $BASE_DIR

EXPOSE ${PORT}

CMD java \
    -Dserver.port=${PORT} \
    -Dcsp.sentinel.dashboard.server=localhost:${PORT} \
    -Dproject.name=sentinel-dashboard \
    -jar sentinel-dashboard-${VERSION}.jar
