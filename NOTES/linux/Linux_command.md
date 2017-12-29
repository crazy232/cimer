### Linux 常用命令

#### 查看端口占用

```shell
$ netstat -tln
$ netstat -tln | grep 8080

# 查看端口属于哪个程序
$ lsof -i :8080

```

#### 开放端口

```shell
# 此种方式在服务器重启后就失效
$ sudo apt-get install iptables
$ sudo iptables -I INPUT -p tcp --dport 80 -j ACCEPT
$ sudo iptables-save

#持久化iptables
$ sudo apt-get install iptables-persistent
$ sudo service iptables-persistent save
```

#### 查看系统版本

```shell
$ lsb_release -a
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.2 LTS
Release:	16.04
Codename:	xenial
```

