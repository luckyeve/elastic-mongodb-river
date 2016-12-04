## 名称：elastic-mongodb-river

## 描述：
 - 环境 jdk 1.8、elasticsearch 5.0.1、mongo 3.2.1
 - 指定要过滤的数据库和表
 - 创建elasticsearch中表映射
 - 启动后，根据filter和mapping指定的表字段读取rs.oplog，写入es。

## 启动
- 配置文件：mrconfig.properties
- 创建库： curl -XPUT localhost:9200/yourdb
- 创建同步的字段： curl -XPUT localhost:9200/yourdb/_mapping/tableName -d '{...}'
- 编译： mvn clean package
- **同步**： java -Dconfig=local -jar mongodb-river.jar
- **初始化**： java -Dconfig=local -jar mongodb-init.jar yourdb.tableName.field>=12345

## mrconfig-{}.properties
    # es
	es.cluster.name=cluster5
    es.transport.address=139.xxx.xxx.80:9300
    es.http.host=192.168.1.12
    es.http.port=6200
    es.http.enable=false

    # mongodb
    mongodb.address=192.168.1.12:27017
    mongodb.dbName=message
    mongodb.username=
    mongodb.password=

    # filter yourdb.tableName
    nosql2es.filter=test\\.feed,test\\.topic

## log4j2.properties、logback.xml

    日志

## oplog.dat

	作用：自动创建，记录最后一次同步的timestamp时间，“oplog.dat”文件默认生成在jar包当前目录下。
    内容：{"time":22223,"inc":22}
