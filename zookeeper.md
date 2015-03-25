# zookeeper 使用 #

## 背景 ##

## ZAB 协议 ##

参考下文
[http://web.stanford.edu/class/cs347/reading/zab.pdf](http://web.stanford.edu/class/cs347/reading/zab.pdf)



![](http://i.imgur.com/GuunAIC.jpg)

## zookeeper 环境搭建 ##
-  创建新用户（可选）

$ sudo groupadd zookeeper
	- 创建一个新的用户，并加入group
	$ sudo useradd -g zookeeper zookeeper
	- 给新用户设置密码
	- $ sudo passwd zookeeper
	
下载解压：
	$ wget http://mirror.bit.edu.cn/apache/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz
	$ tar zxf zookeeper-3.4.5.tar.gz -C /home/zookeeper
启动
	默认就是单机模式
	$ mv conf/zoo_sample.cfg conf/zoo.cfg
	$ ./bin/zdServer.sh start
使用java 客户端连接ZooKeeper
	$ ./bin/zkCli.sh -server 127.0.0.1:2181
关闭

分布式模式
修改配置文件 假设有三台机器（192.168.100.48/49/233)，每台服务器的zoo.cfg增加如下配置
	dataDir=/home/zookeeper/zookeeper-3.4.6/data
	dataLogDir=/home/zookeeper/zookeeper-3.4.6/log
    server.1=192.168.100.48:2888:3888  
    server.2=192.168.100.49:2888:3888  
    server.3=192.168.100.233:2888:3888 

配置myid文件
并在$dataDir 目录下面增加myid的文件，并标志自己的server中配置的ID,例如192.168.100.48机器，那么就在/home/zookeeper/zookeeper-3.4.6/data增加myid文件，并写入1；

查看状态
	/home/zookeeper/zookeeper-3.4.6/bin/zkServer.sh status

客户端连接
	./bin/zkCli.sh -server 192.168.100.48:2888:2181

2. 

## zookeeper 网络连接分析 ##

clientPort=2181

集群配置

    server.1=192.168.100.48:2888:3888  
    server.2=192.168.100.49:2888:3888  
    server.3=192.168.100.233:2888:3888 
----------

    192.168.100.48  Mode: follower
![](http://i.imgur.com/JMkTHLu.png)
 	192.168.100.49  Mode: follower
![](http://i.imgur.com/JGwjZQD.png)
	192.168.100.233 Mode: leader
![](http://i.imgur.com/gAdMfu7.png)

----------


## ZAB C 编码 ##

## ZAB CPP demo ##


```c
int main()
{
	return 0;
}

```
