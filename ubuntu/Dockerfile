FROM ubuntu:16.04

MAINTAINER Mutlu Polatcan <mutlupolatcan@gmail.com>

ENV H2O_HOME "/usr/local/h2o"
ENV JAVA_HOME "/usr/lib/jvm/java-8-openjdk-amd64"
ENV NETWORK_SUBNET "127.0.0.1"

ENV PATH $PATH:$JAVA_HOME/bin

ADD flatfile.txt ./

RUN apt-get update && \
    apt-get -y install --no-install-recommends nano wget unzip default-jre default-jdk && \
    rm -rf /var/lib/apt/lists/* && \
    wget http://h2o-release.s3.amazonaws.com/h2o/rel-wright/1/h2o-3.20.0.1.zip && \
    unzip h2o-3.20.0.1.zip && \
    rm h2o-3.20.0.1.zip && \
    mkdir -p ${H2O_HOME} && \
    mv h2o-3.20.0.1/* ${H2O_HOME} && \
    rm -r h2o-3.20.0.1

EXPOSE 54321
EXPOSE 54322

ENTRYPOINT java -jar ${H2O_HOME}/h2o.jar -network ${NETWORK_SUBNET} -name h2o-cluster -flatfile /flatfile.txt
