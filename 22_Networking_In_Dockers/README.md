# Docker Networks

Create a docker network allowing containers to communicate. Also, focus on Embedded DNS Server added in Docker 1.10.

Docker has two approaches to networking. The first defines a link between two containers. This link updates /etc/hosts and environment variables to allow containers to discover and communicate.

The alternate approach is to create a docker network that containers are connected to. The network has similar attributes to a physical network, allowing containers to come and go more freely than when using links.

### Step 1) Create Networks

* Create a network

```
$ docker network create [network name]
$ docker network ls
```

**Note: Default driver is bridge and scope is local**

* Assign network to container while launching them

```
$ docker run --name=[container name] --net=[network name] [container image]
```

* For example, let's create a **backend-network** with **redis container**.

![Image](img/1.png)

### Step 2) Network Communication

### Step 3) Connect Containers in network

### Step 4) Create Aliases

### Step 5) Disconnect Networks

## References

[Katacoda Scenario](https://www.katacoda.com/courses/docker/networking-intro)
