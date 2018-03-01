### [Macvlan](https://docs.docker.com/engine/userguide/networking/get-started-macvlan/#macvlan-bridge-mode-example-usage) 实施方案实例

#### `macvlan` 不是使用传统的linux网桥进行隔离, 而是简单地与Linux以太网接口或子接口连接,实现网络之间的隔离和物理网络的连接.

#### `macvlan`模式下每个容器的mac地址是唯一的，用于跟踪docker主机端口和容器`mac`地址中间的映射关系

> 1. macvlan 网络连接到Docker宿主机网络接口，例如`eth0`,或者`eth0.10`等子接口
>
>
> 2. 每一个macvlan bridge 模式下的docker网络彼此隔离，一次只能有一个网络连接到父接口，理论上一个父接口可创建4094个子接口
>
>
> 3. 同一子网中的容器通信无需DNS即可通信
>
>
> 4. macvlan子网与子网之间没有外部路由，即不能访问
> 5. macvlan Linux内核要求为v3.9-3.19和4.0+

##### 例1：在下面的例子中，`eth0`docker主机在`172.16.86.0/24`网络上有一个IP 和一个默认网关`172.16.86.1`。网关是一个地址为的外部路由器`172.16.86.1`。`eth0`在`bridge`模式下，Docker主机接口上不需要IP地址，只需要在正确的上游网络上由网络交换机或网络路由器转发即可。

- 此示例中使用的父接口是`eth0`，它在子网上`172.16.86.0/24`。容器中的容器`docker network`也需要与父容器在同一子网上`-o parent=`。网关是网络上的外部路由器，不是任何ip伪装或任何其他本地代理。
  - `container1`和`container2`无法ping通docker宿主机

![](https://docs.docker.com/engine/userguide/networking/images/macvlan_bridge_simple.svg)

##### 例2：有如下网络环境主机

```shell
eth0      Link encap:Ethernet  HWaddr 06:dc:47:1f:a6:2a  
          inet addr:172.16.2.40  Bcast:172.16.2.255  Mask:255.255.255.0
          inet6 addr: fe80::4dc:47ff:fe1f:a62a/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:45305 errors:0 dropped:0 overruns:0 frame:0
          TX packets:28322 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:3620676 (3.6 MB)  TX bytes:6865386 (6.8 MB)
```

- 创建 macvlan网络

```shell
# -d 指定网络模式为macvlan  
# -o 参数代表指定父网络接口,

$ sudo docker network create -d macvlan \
   	--subnet=172.16.2.0/24 \
	--gateway=172.16.2.1 \
	-o parent=eth0 pub_net
	
$ sudo docker network create -d macvlan \ 
    --subnet=172.16.3.0/24 \
    --gateway=172.16.3.1 \
    -o parent=eth0.50 pub_net_low
 
$ sudo docker network create -d macvlan \
    --subnet=172.16.4.0/24 \
    --gateway=172.16.4.1/24 \
    -o parent=eth0.60 pub_net_low
```

- 编写`docker-compose.yml`创建如下docker环境

```shell
version: '2'
services:
    nginx:
        image: "nginx:latest"
        ports:
            - "80:80"
        networks:
            backend:
                ipv4_address: 172.16.2.12
    mysql:
        image: "mysql:5.7"
        ports:
            - "3306:3306"
        environment:
            TZ: 'Asia/Shanghai'
            MYSQL_ROOT_PASSWORD: 'roottoor'
        command: ['mysqld', '--character-set-server=utf8']
        restart: always
        networks:
            backend:
                ipv4_address: 172.16.2.8
         
    kodexplorer:
        image: "1.1.1.3:5000/hp_kodexplorer_a1223"
        ports:
            - "8000:80"
        networks:
            exp_low:
                ipv4_address: 172.16.3.15
    kodexplorer_bak: 
        image: "1.1.1.3:5000/hp_kodexplorer_a1223"
        ports: 
            - "8000:80"
        networks:
            exp_low:
                ipv4_address: 172.16.3.16
    mongodb:
        image: "mongo:latest"
        networks:
            exp_mid:
                ipv4_address: 172.16.4.20
    mongodb_bak:
        image: "mongo:latest"
        networks:
            exp_mid:
                ipv4_address: 172.16.4.21
                
networks:
    backend:
        external:
            name: pub_net
    exp_low:
        external:
            name: pub_net_low
    exp_mid:
        external:
            name: pub_net_mid       
```











