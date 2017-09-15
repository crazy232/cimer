## Connect with the linking system
##### Network port mappings are not the only way Docker containers can connect to another.Docker also has a linking system that allows you to link multiple containers together and send connection information from on to another.When containers are linked,information about a source container can be sent to a recipient container.This allows the recipient to see selected data describing aspects of the source containers.

### The importance of naming
##### To establish links,Docker relies on the names of your containers.You have already seen that each container you create has an automatically created name;indeed you have become familiar with our old friend `notalgic_morse` during this guide.You can alse name containers yourself.This naming provides two useful functions:
##### 1. It can be useful to name containers that do specific functions in a way that makes it easier for you to remember them,for example naming a container containing a web application `web`.
##### 2. It provides Docker with a reference point that allows it to other containers,for example,you can specify to link the containers= `web` to container `db`.
##### You can name your container by using the `--name` flag,for example:
	$sudo docker run -d -p --name web training/webapp python app.py
##### This launches a new container and uses the `--name` flag tp name the container `web`. You can see the container's name using the `sudo docker ps ` command.
	sudo docker ps -l
	CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
	0b8ef9840de0        training/webapp     "python app.py"     5 minutes ago       Up 5 minutes        0.0.0.0:32768->5000/tcp   web
##### You can also use `docker inspect` to return the container's name.

### Communication across links
##### Links allow containers to discover each other securely transfer information about one container to another container.When you set up alink ,you create a conduit between a source container and a recipient container.The recipient canthen access select data about the source.To create a link,you use the `--link` flag.First,create a new container,this time one containing a database.
	sudo docker run -d --name db training/postgres
##### This creates a new container called `db` from the `training/postgres` image,which contains a PostgreSQL database.
##### Now,you need to delete the `web` container you created previously so you can replace it eith a linked one:
	sudo docker rm -f web
