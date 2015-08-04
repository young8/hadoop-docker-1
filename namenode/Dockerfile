FROM hadoop/base

MAINTAINER Byron Yi <byi@connect.ust.hk>

RUN $HADOOP_HOME/bin/hdfs namenode -format

EXPOSE 50010 50020 50070 50075 50090

ENTRYPOINT ["/hadoop/bin/hdfs", "namenode"]
