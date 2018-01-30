### Dockerfile 常用语句

```shell
# 更新apt-get源
sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list 
sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g'  /etc/apt/sources.list

# 更新debian源
echo "deb http://mirrors.163.com/debian wheezy main non-free contrib" > /etc/apt/sources.list
echo 'deb http://deb.debian.org/debian stretch main' > /etc/apt/sources.list.d/stretch.list
```

```shell
# 163 ubuntu 源
deb http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse
```
```shell
# 163 debian源
deb http://mirrors.163.com/debian wheezy main non-free contrib
deb http://mirrors.163.com/debian wheezy-proposed-updates main contrib non-free
deb http://mirrors.163.com/debian-security wheezy/updates main contrib non-free 
deb-src http://mirrors.163.com/debian wheezy main non-free contrib
deb-src http://mirrors.163.com/debian wheezy-proposed-updates main contrib non-free
deb-src http://mirrors.163.com/debian-security wheezy/updates main contrib non-free 

deb http://http.us.debian.org/debian wheezy main contrib non-free
deb http://non-us.debian.org/debian-non-US wheezy/non-US main contrib non-free
deb http://security.debian.org wheezy/updates main contrib non-free

```

```shell
# ustc ubuntu源
deb http://debian.ustc.edu.cn/ubuntu/ trusty main multiverse restricted universe
deb http://debian.ustc.edu.cn/ubuntu/ trusty-backports main multiverse restricted universe
deb http://debian.ustc.edu.cn/ubuntu/ trusty-proposed main multiverse restricted universe
deb http://debian.ustc.edu.cn/ubuntu/ trusty-security main multiverse restricted universe
deb http://debian.ustc.edu.cn/ubuntu/ trusty-updates main multiverse restricted universe
deb-src http://debian.ustc.edu.cn/ubuntu/ trusty main multiverse restricted universe
deb-src http://debian.ustc.edu.cn/ubuntu/ trusty-backports main multiverse restricted universe
deb-src http://debian.ustc.edu.cn/ubuntu/ trusty-proposed main multiverse restricted universe
deb-src http://debian.ustc.edu.cn/ubuntu/ trusty-security main multiverse restricted universe
deb-src http://debian.ustc.edu.cn/ubuntu/ trusty-updates main multiverse restricted universe
```
```shell
# aliyun Ubuntu源
deb http://mirrors.aliyun.com/ubuntu/ version main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ version-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ version-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ version-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ version-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ version main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ version-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ version-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ version-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ version-backports main restricted universe multiverse
```
```shell
# aliyun debian源
deb http://mirrors.aliyun.com/debian/ wheezy main non-free contrib
deb http://mirrors.aliyun.com/debian/ wheezy-proposed-updates main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ wheezy main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ wheezy-proposed-updates main non-free contrib
```
```shell
# 卸载已安装包
apt-get purge -y --auto-remove ca-certificates wget
```

```shell
# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
```


