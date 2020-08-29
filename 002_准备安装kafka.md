# 002_准备安装kafka



## 1th 安装java

```
yum -y install java-1.8.0-openjdk.x86_64
```





```
yum install iproute ftp bind-utils net-tools wget -y

分开运行
yum install net-too
ls -y
yum install wget -y
```

其中:
iproute 用来执行 ip address 查看本机地址
ftp 用来测试ftp 服务器
bind_utils 用来运行 nslookup
net-tools 用来执行 netstate
wget 既是执行 wget的



```
netstat -anp|grep 8080

wget http://how2j.cn

nslookup www.baidu.com
```





## 2th 安装zookeeper

tar -zxf zookeeper-3.4.14.tar.gz



tickTime=2000
dataDir=/usr/local/zookeeper-3.4.10/data
clientPort=2181
initLimit=5
syncLimit=2



cp zoo_sample.cfg zoo.cfg

vi zoo.cfg

cat zoo.cfg

./zkServer.sh start **开启zookeeper**

./zkServer.sh stop **关闭zookeeper**

./zkCli.sh





## 3th kafka使用



### **启动kafka**

./kafka-server-start.sh ../config/server.properties



./kafka-server-stop.sh ../config/server.properties

- 在kafka的bean目录里执行



### 新建主题

语法:

```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 
--partitions 1 --topic topic-name
```

实例

```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1
--partitions 1 --topic Hello-Kafka
```

- 需要在kafka目录里执行



### 查看Kafka里的所有主题

```
bin/kafka-topics.sh --list --zookeeper localhost:2181
```

- 同样需要在kafka目录里执行



![1597796719668](small1ddd_doc_mdmd_pic/1597796719668.png) 

---

### 生产数据

语法 

bin/kafka-console-producer.sh --broker-list localhost:9092 --topic topic-name

示例

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic Hello-Kafka
```



显示效果

![1597797374499](small1ddd_doc_mdmd_pic/1597797374499.png) 









---

### 消费数据 



语法

```
bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic topic-name --from-beginning
```



示例

```
bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic Hello-Kafka --from-beginning
```

此处报了一个错误,是版本的问题,这个命令是老版本的命令,新版本的kafka参数做了修改.

- **命令修改后**

bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic Hello-Kafka --from-beginning



![1597797897095](small1ddd_doc_mdmd_pic/1597797897095.png)  

- 看到了从生产者中发出的数据
- 注意以后命令中的参数把localhost修改为虚机的ip[192.168.222.142]

---



shutdown -h now



## 4th spring操作kafka

修改kafka里的server.properties

vi server.properties

在listeners里加入ip地址

listeners=PLAINTEXT://9092--->listeners=PLAINTEXT://192.168.222.142:9092

```
listeners=PLAINTEXT://192.168.222.142:9092

```



## 打开9092端口

firewall-cmd --add-port=9092/tcp --permanent

firewall-cmd --reload

firewall-cmd --list-ports

重启网络服务

systemctl restart firewalld.service

---



- 运行**KfkSpringProducer**.java 生产者发送数据到kafka

![1597801296877](small1ddd_doc_mdmd_pic/1597801296877.png) 

在kafka消费则者窗口能够查看到发送的数据

![1597801393775](small1ddd_doc_mdmd_pic/1597801393775.png) 

- 注意bootstrap-server 的参数不是localhost,而是虚拟机的IP了
- 即192.168.222.142
- 因为我们修改了server.properties

消费者效果图

![1597823601484](small1ddd_doc_mdmd_pic/1597823601484.png) 



**用main函数启动项目即可**







```
find -name "*kafka*"
find -name "*zookeeper*"
```



---

- 





















