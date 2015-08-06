FROM ubuntu
MAINTAINER Byron Yi <byi@connect.ust.hk>

RUN apt-get update && apt-get install -y curl

RUN mkdir -p /java && curl -kL -b "oraclelicense=a" \
http://download.oracle.com/otn-pub/java/jdk/7u80-b15/jdk-7u80-linux-x64.tar.gz \
| tar -xz --strip-components=1 -C /java

RUN mkdir -p /hadoop && curl -kL \
http://www.us.apache.org/dist/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz \
| tar -xz --strip-components=1 -C /hadoop

ENV JAVA_HOME /java
ENV HADOOP_HOME /hadoop
ENV HADOOP_CONF_DIR /conf
