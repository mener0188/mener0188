# 003_linux命令总结



## 0th





## 1th firewall

> firewall-cmd命令
>
> - firewall-cmd --list-ports 
> - firewall-cmd --add-port=9092/tcp --permanent
>   - --permanent 参数必须加
> - man firewall-cmd
>   - 开启一个端口号后,一定要用reload重新加载,否则不生效
> - firewall-cmd --reload
> - firewall-cmd --remove-port=9092/tcp
>   - 关闭端口





## 2th netstat -lnpt

- 2181端口和9092端口被占用 



> - 案例,,,当zookeeper死机之后,用命令关闭zookeeper不好使
> - 这是需要用kill -9来结束进程,同时配合netstat -lnpt来查看效果
> - 不用netstat -lnpt命令无法查看效果,因为zookeeper已经死机,zookeeper命令都没有反应了

命令总结如下

netstat -lnpt | grep 2181

kill -9 2181



## 3th 其他



```
whereis java
whereis redis
```











End