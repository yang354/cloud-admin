FROM openjdk:8-jdk
LABEL maintainer=yyyz


#docker run -e PARAMS="--server.port 9090"
ENV PARAMS="--server.port=8080 --spring.profiles.active=prod --spring.cloud.nacos.discovery.server-addr=ruoyi-nacos.yyz-ruoyi:8848 --spring.cloud.nacos.config.server-addr=ruoyi-nacos.yyz-ruoyi:8848 --spring.cloud.nacos.config.namespace=prod --spring.cloud.nacos.config.file-extension=yml"
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

COPY target/*.jar /app.jar
EXPOSE 8080

#
ENTRYPOINT ["/bin/sh","-c","java -Djava.security.egd=file:/dev/./urandom -jar app.jar ${PARAMS}"]
