FROM hadoop/base

MAINTAINER Byron Yi <byi@connect.ust.hk>

RUN apt-get update && apt-get install -y \
ipython ipython-notebook python python-numpy python-scipy \
python-matplotlib python-pandas python-sklearn

RUN mkdir -p /spark && curl -kL \
http://www.us.apache.org/dist/spark/spark-1.4.1/spark-1.4.1-bin-hadoop2.6.tgz \
| tar -xz --strip-components 1 -C /spark

ENV SPARK_CONF_DIR /conf

EXPOSE 4040 7001-7006 7070 8080 8081 18080
