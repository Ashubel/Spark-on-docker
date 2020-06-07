# Spark-on-docker
Docker搭建Spark集群

0x01 下载Dockerfile

0x02 在Dockerfile所在目录构建镜像`docker build -t spark:v3.0.0 . `

0x03 当镜像构建成功后，直接开启`spark-master`
` docker run -itd --name spark-master -p 6066:6066 -p 7077:7077 -p 8081:8080 -h spark-master spark:v2.4.0 ./bin/spark-class org.apache.spark.deploy.master.Master`

0x04 开启`spark-worker`
`docker run -itd --name spark-worker -P -h spark-worker --link spark-master spark:v3.0.0 ./bin/spark-class org.apache.spark.deploy.worker.Worker spark://spark-master:7077`

0x05 执行`docker ps -a`获取容器运行状态以及容器id

0x06 执行`docker exec -it '容器id' ./bin/spark-shell`进入容器
