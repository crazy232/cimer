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
#### 清除history
```shell
$ history -c 
$ echo ""> ./.bash_history
```
#### 清除last
```shell
$ echo "">/var/log/wtmp
```
#### 查看CPU 核数
> CPU总核数 = 物理CPU个数 * 每颗物理CPU的核数 
  总逻辑CPU数 = 物理CPU个数 * 每颗物理CPU的核数 * 超线程数
```shell
# 查看CPU型号
$ cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
# 查看物理CPU个数
$ cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l
# 查看每个物理CPU核数
$ cat /proc/cpuinfo| grep "cpu cores"| uniq
# 查看逻辑CPU个数
$ cat /proc/cpuinfo| grep "processor"| wc -l
```
