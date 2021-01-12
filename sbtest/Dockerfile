FROM cargo.caicloudprivatetest.com/caicloud/centos7jdk1.8

ENV JAVA_OPTS="-Djava.awt.headless=true -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=10053 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false"
ENV LOG_FOLDER=/data0/logs/

COPY app.jar app.jar

RUN mkdir -p $LOG_FOLDER

EXPOSE 8080
EXPOSE 10053

ENTRYPOINT ["./app.jar", "start"]