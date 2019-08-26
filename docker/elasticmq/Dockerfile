FROM debian:buster-slim

ENV ELASTICMQ_VERSION 0.14.10
RUN apt-get update \
    # https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199#23
    && mkdir -p /usr/share/man/man1 \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        apt-transport-https \
        curl \
        openjdk-11-jre \
    && rm -rf /var/lib/apt/lists/* \
    && curl -sS -o elasticmq-server.jar https://s3-eu-west-1.amazonaws.com/softwaremill-public/elasticmq-server-${ELASTICMQ_VERSION}.jar

ADD ./conf/custom.conf /

EXPOSE 9324

ENTRYPOINT [ "java" ]
CMD [ "-Dconfig.file=custom.conf", "-jar", "elasticmq-server.jar" ]