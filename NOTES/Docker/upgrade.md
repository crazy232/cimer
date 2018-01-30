- 升级docker到最新版本

```shell
$ sudo apt-get update
$ sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu    	$(lsb_release -cs) stable"
$ sudo apt-get update
$ sudo apt-cache madison docker-ce
$ sudo apt-get -y install docker-ce=[VERSION]
$ sudo docker --version
```

- 卸载docker

```shell
$ sudo apt-get remove docker docker-engine
$ sudo rm -rf /var/lib/docker/
```

