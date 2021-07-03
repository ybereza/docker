FROM ubuntu:20.04
MAINTAINER ybereza

ARG JDK_VER=11.0.2
ARG ZOOKEEPER_VER=3.6.3

RUN apt-get update && apt-get -y upgrade && apt-get -y install wget tar

# Install Java. At this time Zookeeper supports JDK 11
ENV JAVA_HOME /usr/lib/jvm/jdk-${JDK_VER}
ENV PATH $PATH:$JAVA_HOME/bin

RUN mkdir -p /usr/lib/jvm
WORKDIR /usr/lib/jvm
RUN wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-${JDK_VER}_linux-x64_bin.tar.gz
RUN tar -xf openjdk-${JDK_VER}_linux-x64_bin.tar.gz
RUN rm openjdk-${JDK_VER}_linux-x64_bin.tar.gz

# Install Zookeeper
WORKDIR /usr/lib
RUN wget https://apache-mirror.rbc.ru/pub/apache/zookeeper/zookeeper-${ZOOKEEPER_VER}/apache-zookeeper-${ZOOKEEPER_VER}-bin.tar.gz
RUN tar -xf apache-zookeeper-${ZOOKEEPER_VER}-bin.tar.gz
RUN rm apache-zookeeper-${ZOOKEEPER_VER}-bin.tar.gz
RUN mv apache-zookeeper-${ZOOKEEPER_VER}-bin zookeeper
RUN cp /usr/lib/zookeeper/conf/zoo_sample.cfg /usr/lib/zookeeper/conf/zoo.cfg
RUN chmod +x /usr/lib/zookeeper/bin/zkServer.sh

EXPOSE 2181

CMD ["/usr/lib/zookeeper/bin/zkServer.sh", "start-foreground"]
