
![Untitled 3](../../assets/Untitled%203.png)


When you need to communicate between two or more containers, you need to specify the url for docker

  

> [!important]  
> Instead this: mongodb://localhost:27017/swfavoritesUse thismongodb://host.docker.internal:27017/swfavorites  

  

![Untitled 1 2](../../assets/Untitled%201%202.png)

  

First of all, we need to create a network node

```JavaScript
docker network create <some-network-name>
```

  

To add some container on this network node, just add `--network <your-network-name>`, follow the example below:

```JavaScript
docker run -d --name mongodb --network favorites-net mongo
```

  

Now, the container named Mongodb is in favorites-net network node.

  

### **Docker Network Drivers**

Docker Networks actually support different kinds of "**Drivers**" which influence the behavior of the Network.

The default driver is the "**bridge**" driver - it provides the behavior shown in this module (i.e. Containers can find each other by name if they are in the same Network).

The driver can be set when a Network is created, simply by adding the `--driver` option.

  

> [!important]  
> Of course, if you want to use the "bridge" driver, you can simply omit the entire option since "bridge" is the default anyway.  

  

Docker also supports these alternative drivers - though you will use the "bridge" driver in most cases:

- **host**: For standalone containers, isolation between the container and host system is removed (i.e. they share `localhost` as a network)
- **overlay**: Multiple Docker daemons (i.e. Docker running on different machines) can connect with each other. Only works in "Swarm" mode which is a dated / almost deprecated way of connecting multiple containers
- **macvlan**: You can set a custom MAC address to a container - this address can then be used for communication with that container
- **none**: All networking is disabled.
- **Third-party plugins**: You can install third-party plugins which then may add all kinds of behaviors and functionalities

As mentioned, the "**bridge**" driver makes most sense in the vast majority of scenarios.