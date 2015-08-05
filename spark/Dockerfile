FROM hadoop/base

MAINTAINER Byron Yi <byi@connect.ust.hk>

RUN mkdir -p /spark && curl -kL \
http://d3kbcqa49mib13.cloudfront.net/spark-1.4.1-bin-hadoop2.6.tgz \
| tar -xz --strip-components 1 -C /spark
