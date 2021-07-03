FROM ubuntu:20.04
MAINTAINER ybereza

ARG JDK_VER=11.0.2
ARG KAFKA_VER=2.8.0

RUN apt-get update && apt-get -y upgrade && apt-get -y install wget tar

# Install Java. At this time Zookeeper supports JDK 11
ENV JAVA_HOME /usr/lib/jvm/jdk-${JDK_VER}
ENV PATH $PATH:$JAVA_HOME/bin

RUN mkdir -p /usr/lib/jvm
WORKDIR /usr/lib/jvm
RUN wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-${JDK_VER}_linux-x64_bin.tar.gz
RUN tar -xf openjdk-${JDK_VER}_linux-x64_bin.tar.gz
RUN rm openjdk-${JDK_VER}_linux-x64_bin.tar.gz

# Install Kafka
WORKDIR /usr/lib
RUN wget https://apache-mirror.rbc.ru/pub/apache/kafka/${KAFKA_VER}/kafka_2.13-${KAFKA_VER}.tgz
RUN tar -xf kafka_2.13-${KAFKA_VER}.tgz
RUN rm kafka_2.13-${KAFKA_VER}.tgz
RUN mv kafka_2.13-${KAFKA_VER} kafka
RUN chmod +x /usr/lib/kafka/bin/kafka-server-start.sh
COPY ./config/ ./kafka/config/
RUN mkdir -p /tmp/kafka-logs

EXPOSE 7203
EXPOSE 9092

CMD ["/usr/lib/kafka/bin/kafka-server-start.sh", "/usr/lib/kafka/config/server.properties"]
