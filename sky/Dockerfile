FROM alpine:3.9
MAINTAINER docker-build
ENV LANG=C.UTF-8 \
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk \
    PATH=$PATH:/usr/lib/jvm/java-1.8.0-openjdk/jre/bin \
    run_foreground=true
RUN apk add --no-cache openjdk8 && rm -f /etc/apk/repositories
RUN mkdir  /skywalking
# 需要skywalking-agent.jar
ADD ./skywalking /skywalking
