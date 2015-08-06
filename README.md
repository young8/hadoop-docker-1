Containerized Hadoop
===

Requirements
---
Docker 1.8.0-dev


Build the Images
---
```bash
for image in base namenode datanode resourcemanager nodemanager;
do
  docker build -t hadoop/$image $image
done
```

Deploy the Containers
---
```bash
docker run -d -v `pwd`/conf:/conf -p 50070:50070 --name namenode -h namenode --publish-service namenode.hadoop hadoop/namenode
for i in `seq 1 3`;
do
  docker run -d -v `pwd`/conf:/conf --name datanode$i -h datanode$i --publish-service datanode$i.hadoop hadoop/datanode
done

docker run -d -v `pwd`/conf:/conf -p 8088:8088 --name resourcemanager -h resourcemanager --publish-service resourcemanager.hadoop hadoop/resourcemanager
for i in `seq 1 5`;
do
  docker run -d -v `pwd`/conf:/conf --name nodemanager$i -h nodemanager$i --publish-service nodemanager$i.hadoop hadoop/nodemanager
done
```

Hello World
---
```bash
docker run -it --rm -v `pwd`/conf:/conf -h client --publish-service client.hadoop hadoop/base bash -c "/hadoop/bin/yarn jar /hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.1.jar pi 16 10000000"
```
And you can open ``http://localhost:8088`` to monitor the running application.

Hadoop Configuration
---
Change them as you wish in ``conf`` folder. Currently I found it most convenient to attach them as a separate volume instead of baked them into the image. Let me know if you have a better idea!

SWIM Traffic Replay
---
Modify the SWIM Dockerfile and build the SWIM docker image first, and run
```bash
docker build -t hadoop/swim swim
docker run -it --rm -v `pwd`/conf:/conf --publish-service swim.hadoop --name swim -h swim hadoop/swim
```
