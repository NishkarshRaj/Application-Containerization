## Docker compose

* Docker-compose is used to run multiple containers in a cluster that are dependent on each other. It is an alternative to Docker Swarm and Kubernetes but generally used for preferably small clusters.

* All the containers to be used are defined together in a configuration file called **docker-compose.yaml**

* YAML - Yet Another Markup Language

**Example: Docker-Compose.yaml file**

```yaml
web:
  build: .
  links:
    - redis
  ports:
    - "3000"
    - "8000"

redis:
  image: redis:alpine
  volumes:
    - /var/redis/data:/data
```

**Explanation:** Here we launch a NodeJS web application connected to Redis database.
* Format is 
```yaml
container_name:
  property:
    - value
```
* First container called web is defined and uses a Dockerfile of NodeJS in the build path . (current folder)

* Dockerfile for NodeJS application

```Dockerfile
FROM ocelotuproar/alpine-node:5.7.1-onbuild
EXPOSE 3000
```

* **links** keyword is used to link one container in the yaml to another, it can be anything but it must be defined as a container name in the same file.

* Second container is of key-value database called **Redis**

* It is defined using Redis image from DockerHub

* Volume is mapped from the linked Node.JS container to the current container.

## Docker-compose commands

* Launch the cluster

```
$ docker-compose up -d # for detached mode
```

* Check the state of containers in the cluster

```
$ docker-compose ps
```

* Check logs of the cluster

```
$ docker-compose logs
```

* Scale up/down a specific cluster of the container

```
$ docker-compose scale [container-name]=replicals [container-name]=replicas ...
```

* Stop all the containers of the cluster

```
$ docker-compose stop
```

* Remove all containers of the cluster

```
$ docker-compose rm
```


