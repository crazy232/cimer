# docker container networking 
## networking on single host
### docker can provide isolated network environments for containers based on the control of net namespace. Containers have completed independent network stack from host,containers can also share net namespace of host and other containers,so it meets the needs of developers in many occasions. 
### The are five modes of container networking:


- bridge: the default networking mode,docker build independent net namespace for containers,that possess independent network stack,which is the most common way.
- host:containers share the same net namespace with host.
- none:docker creates new net namespace for containers without any configuration,developers can custom network as wish.
- dependence:containers will share net namespace with others.
- self-define:after the docker v1.9, docker allows containers use third party networking or create independent bridge networking,providing environment of isolated.

----------
### Let's take a closer look at the details of those modes
### host
#### Thanks to containers share the same net namespace with host,so does the ip address,containers can use the alternative network card to communicate with outside,the network model can refer to the following image:
![](http://www.skycloudsoftware.com/wp-content/uploads/docker%E8%AF%A6%E8%A7%A301.jpg?_=6680205)
#### The ports run by services in containers can use the ports of host directly without NET translation.It have a great performance due to no need to pass through Linxbridge or packet forwarding.Of course,the mode also has disadvantages,mainly including the following aspects:
##### 1. The most obvious is that the container no longer has a separate and independent network stack.The container will compete with the host for the use of network stack,and the collapse of the container may cause the host to crash,which is not allowed in the production environment.
##### 2.The container will no longer have all the port resources,because some ports have been occupied by the host services or port binding in the bridge mode and other services.

### bridge
#### This is the default mode in docker and the most common net mode for developers.docker build independent network stack for processes running in a isolated environment.In the case,containers can communicate to outside through the `docker0` bridge.The network model can refer to the following image:
![](http://www.skycloudsoftware.com/wp-content/uploads/docker%E8%AF%A6%E8%A7%A302.jpg?_=6680205)
#### containers can connect to the bridge docker0 which serve as a visual switch on the same host.Because host IP distribute in the different range with veth pair IP in container,it is not enough for outside to find the exist of container only depending on the technology of veth pair and namespace.For exposing the processes in containers to outside,docker adopt the way of port binding,it forwards flow from ports on host to containers via the NAT of iptables.
#### For example,create a container with the following commands,and bind the 3306 of host to 3306 in container:
    sudo docker run -itd --name db -p 3306:3306 mysql:5.7
#### We can find a DNAT rule by `iptables -t nat -L -n` on host
    sudo iptables -t nat -L -n
	target     prot opt source               destination 
	DNAT       tcp  --  0.0.0.0/0            127.0.0.1            tcp dpt:1514 to:172.18.0.7:514
#### Obviously,it must occupy ports on host in the bridge mode,resulting in consuming port resources make it hard to manage resources of host.In addition,it will reduce the performance and efficiency because the communication is based on iptables NAT above three lays.

### none
####containers will have independent network stack without any special net configuration but only the `lo`(loopwork)network card is working for process communication.In this word,this mode cut out the minimum configuration.So it's free for developers to custom the container network as wish by using three-party tools with the `none` configuration ,that providing the highest flexibility.

### dependence
#### Containers will communicate with others net namespace,so the isolation between containers will gone,and the isolation with host is still exist,The network model can refer to the following image:<br>
![](http://www.skycloudsoftware.com/wp-content/uploads/docker%E8%AF%A6%E8%A7%A303.jpg?_=6680205)
#### Containers can communicate with the net namespace `localhost` with high transmission efficiency in this mode,that also save the network resources but not change the way of communication.It works a lot in some special occasion,such as, `pod` in `Kubernetes`, in this case,`Kubernetes` create a container to serve as a infrastructure,and other containers can share the net namespace of that under the same `pod`,they unit as a whole body. 

### self-define
#### Developers can use any driver that docker support for third party networks to build container network.Docker support the default driver of `bridge` and `overlay` after `docker1.9`.Developers can concordance third party vendors such as ` calico`,` weave`,` openvswitch` to build their own networks.
