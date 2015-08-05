FROM hadoop/base

RUN mkdir -p /swim

RUN curl -kL \
https://github.com/SWIMProjectUCB/SWIM/archive/master.tar.gz \
| tar -xz --strip-components 2 -C /swim

ENV PATH $JAVA_HOME/bin:$HADOOP_HOME/bin:$PATH

WORKDIR /swim

RUN javac GenerateReplayScript.java

RUN yes | java GenerateReplayScript \
FB-2009_samples_24_times_1hr_0_first50jobs.tsv \
100 \
5 \
67108864 \
10 \
scriptsTest \
workGenInput \
workGenOutputTest \
67108864 \
workGenLogs \
hadoop \
WorkGen.jar \
'/conf/workGenKeyValue_conf.xsl'

RUN mkdir -p hdfsWrite
RUN mkdir -p workGen

RUN javac -classpath `hadoop classpath` -d hdfsWrite HDFSWrite.java
RUN javac -classpath `hadoop classpath` -d workGen WorkGen.java

RUN jar -cvf HDFSWrite.jar -C hdfsWrite/ .
RUN jar -cvf WorkGen.jar -C workGen/ .

RUN cp HDFSWrite.jar WorkGen.jar scriptsTest/

WORKDIR scriptsTest/

CMD hdfs dfs -rmr workGenInput && \
yarn jar HDFSWrite.jar org.apache.hadoop.examples.HDFSWrite -conf /conf/randomwriter_conf.xsl workGenInput && \
./run-jobs-all.sh
