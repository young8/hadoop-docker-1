FROM hadoop/spark

MAINTAINER Byron Yi <byi@connect.ust.hk>

ENV MASTER yarn-client
ENV PYSPARK_DRIVER_PYTHON ipython
ENV PYSPARK_DRIVER_PYTHON_OPTS notebook --ip=* --port 8888 --no-browser

EXPOSE 8888

ENTRYPOINT /spark/bin/pyspark
