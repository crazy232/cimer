### `Docker`常用技巧

-  配置加速器
```shell
# 加速器地址参考https://cr.console.aliyun.com/?spm=5176.100239.blogcont29941.12.sNabT2#/accelerator
$ echo "DOCKER_OPTS="--registry-mirror=https://****.mirror.aliyuncs.com"" >> /etc/default/docker
```
- 仓库使用
```shell
# 当push镜像到仓库时可能出现
# Get https://ip:5000/v1/_ping: http: server gave HTTP response to HTTPS client
# 需要额外配置参数

# ubuntu 配置push到仓库
$ echo "DOCKER_OPTS="$DOCKER_OPTS --insecure-registry=http://ip:5000"" >> /etc/default/docker
$ service docker restart

# CentOS配置push到仓库
# 在/etc/docker目录下创建daemon.json,写入如下内容：
{ "insecure-registries" : ["ip:5000"] }
$ service docker restart
```
- 在宿主机中查看容器CPU,内存，网络,IO等占用情况
```
$ sudo docker stats CONTAINERID
CONTAINER           CPU %               MEM USAGE / LIMIT       MEM %               NET I/O               BLOCK I/O             PIDS
elasticsearch       119.21%             490.5 MiB / 3.854 GiB   12.43%              248.6 MB / 258.8 MB   405.3 MB / 28.16 MB   79
```
- `Docker daemon`日志文件位置

> Ubuntu - /var/log/upstart/docker.log
>
> Boot2Docker - /var/log/docker.log
>
> Debian GNU/Linux - /var/log/daemon.log
>
> CentOS - /var/log/daemon.log | grep docker
>
> Fedora - journalctl -u docker.service
>
> Red Hat Enterprise Linux Server - /var/log/messages | grep docker

- 设置容器时区

```shell
# 创建时以环境变量传递进去
$ docker run -itd --name test -e TZ='Asia/Shanghai' images

# 单纯使用环境变量传递time zone 只对当前容器用户的时区影响, 一旦切换到root用户，时区就会出错

# 真正解决办法是修改/etc/localtime,可以在容器内部执行已下命令，也可在制作镜像时,将这句话写入Dockerfile
$ ls -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

- 快速管理容器和镜像

```shell
# 输出所用容器名字
$ sudo docker ps --format='{{.Names}}'
 
# 输出所有容器名包含test的容器，并打印容器名
$ sudo docker ps -f name=test --format='{{.Names}}'

# 查看退出状态容器
$ sudo docker ps -f status=exited --format="{{.Names}}"

# 删除所有退出状态容器
$ sudo docker rm -f $(sudo docker ps -f status=exited)

# 删除所有镜像
$ sudo docker rmi -f $(sudo docker images -q)

# 只列出容器的相关id,image,status和name
$ sudo docker ps --format "{{.ID}}: {{.Image}} : {{.Status}} : {{.Names}}"
```

- 使用容器`label`

```shell
#在实际运维过程中，大量的容器可能会一些运维上的挑战，通过使用label，可以很好的将容器分类。label贯穿于
#docker的整个过程。
#这个label可以作为你区分业务，区分模板各种区分容器的标识，通过标识，可以将容器更好的进行分组

$ sudo docker run -itd --name=test --label zone=test alpine /bin/sh
# 通过label查看容器
$ sudo docker ps -qf label=zone=test
```

- 快速查看容器信息

```shell
# 查看容器的devicemapper设备：
$ docker inspect -f '{{.GraphDriver.Data.DeviceName}}' nginx 

# 查看容器的PID：
$ docker inspect -f '{{.State.Pid}}' nginx 

# 查看容器name：
$ docker inspect -f '{{.Name}}' nginx 

# 获取容器的ID：
$ docker inspect --format {{.Id}} nginx

```

- 使用`alias`预定义命令别名

```shell
$ alias dockerm='docker rm -f -v'
$ sudo dockerm test
```

- 给容器配置hosts

```shell
$ sudo docker run --add-host www.test.com:192.168.5.3 centos cat /etc/hosts
```

