
```docker

FROM openjdk:8u151-alpine
LABEL maintainer="liguobao <codelover@qq.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV JAVA_OPTS "-Xms256M -Xmx512M"
ENV SKYWALKING_COLLECTOR_OPTS ""
ENV SKYWALKING_HOME /usr/local/skywalking-collector
ENV SKYWALKING_CONFIG_DIR ${SKYWALKING_HOME}/config
ENV SKYWALKING_CLASSPATH "${SKYWALKING_HOME}/collector-libs/*:${SKYWALKING_CONFIG_DIR}"
ENV ES_HOST=10.
COPY . /usr/local/skywalking-collector/
RUN chmod -R 777 ${SKYWALKING_HOME} \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone
EXPOSE 10800 11800 12800
CMD java ${JAVA_OPTS} ${SKYWALKING_COLLECTOR_OPTS} -classpath ${SKYWALKING_CLASSPATH} org.apache.skywalking.apm.collector.boot.CollectorBootStartUp
```