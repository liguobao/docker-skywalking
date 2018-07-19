```docker
FROM openjdk:8u151-alpine
ENV MY_HOME=/usr/src/app
RUN mkdir -p $MY_HOME
WORKDIR $MY_HOME
COPY . .
EXPOSE 8080
ENV COLLECTOR_HOST=http://skywalking-collector:10800
CMD java -jar ./webapp/skywalking-webapp.jar --server.port=8080 --collector.ribbon.listOfServers=${COLLECTOR_HOST} --collector.ribbon.ReadTimeout=10000 

```