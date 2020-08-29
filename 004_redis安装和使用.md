# 004_redis安装和使用



## 0th

redis介绍

redis是非常常用的内存数据库



## 1th 安装gcc

- redis是c语言编写的,安装redis,需要安装gcc编译器
- yum install gcc-c++ -y
- 桌面版本的cetos7系统自带gcc-c++

最后安装成功截图

![1597885457137](../../small1/ddd_doc_md/md_pic/1597885457137.png) 

---



## 2th 安装redis

```
wget http://download.redis.io/releases/redis-2.8.17.tar.gz
```

```
tar xzf redis-2.8.17.tar.gz
```

```
cd redis-2.8.17
```

```
make
```

1. 用 tar -zxf
2. 用wget不用拖jar包到虚机里了



make 效果成功截图:

![1597885851314](../../small1/ddd_doc_md/md_pic/1597885851314.png) 



## 3th 启动redis

启动redis-server的两种方式[^注1]



- ./redis-server

![1597885198726](../../small1/ddd_doc_md/md_pic/1597885198726.png) 

- ./redis-server ../redis.conf

![1597885239809](../../small1/ddd_doc_md/md_pic/1597885239809.png) 

成功启动redis截图

![1597885993075](../../small1/ddd_doc_md/md_pic/1597885993075.png) 



---

要想启动redis-cli必须先启动redis_server

- 启动redis-cli

![1597885301055](../../small1/ddd_doc_md/md_pic/1597885301055.png) 

./redis-cli

运行成功截图

![1597886545363](../../small1/ddd_doc_md/md_pic/1597886545363.png) 

redis常用命令

- keys *
- set foo msg
- get foo
- ping
- 等等
- 6379是redis的端口号

## 把linux的6379端口号打开

>firewall-cmd --list-ports
>
>firewall-cmd --add-port=6379/tcp --permanent
>
>firewall-cmd --reload



执行make命令后,还可以执行make install

执行make install后会把redis-server,reids-cli等命令安装到系统的默认路径中

```java
find -name "*redis*"
```

from below, find the directory of redis, is /usr/local/bin

![1597889436567](../../small1/ddd_doc_md/md_pic/1597889436567.png) 

在linux的根目录里执行redis-server,redis-cli命令即可



## 4th redisTemplate使用

>RedisTemplate redisTemplate=(RedisTemplate) context.getBean("redisTemplate");
>
>redisTemplate.opsForValue().set("x1", "hello x1");
>
>redisTemplate.opsForValue().get("x1")



---

+++

---

---

end

[^注1]: 第一种是常用的方式,第二种不常用