## Basics on Docker on Ubuntu virtual machine using Vagrant

**1. Launch Ubunut VM via Vagrant on command line**

```
$ vagrant up
```

**2. Up a vagran box on vagrant**
```
$ vagrant ssh
```
**3. Install docker on the virtual machine**
```
$ sudo apt install docker.io
```
**4. Pull the most basic Linux image: Alpine**
```
$ docker pull alpine
```

**5. Run Alpine container**
```
$ docker run alpine
```

> Run command only exectues container which destroys itself after executing all its tasks.

**6. Go inside container terminal using Interactive mode**

```
$ docker run -it alpine 
```
* **-i:** Interactive
* **-t:** Terminal

**7. Send a running container in detached mode: Running but not interacted with**

`ctrl + p + s` 

> To stop an up and running container  

* Find the container name or ID by using `docker ps`
```
$ docker stop <container name>
```

After stop command, container is destroyed and it moves into exit state.
All the exited containers can be seen through `docker ps -a` command.

**8. Restart the exited container in up and running state**
```
$ docker start container-id 
```
**9. Execute linux command in container using alpine shell**

```
$ docker run -it alpine /bin/sh
```

**10. Delete containers: remove exited containers from memory so that they are inaccessible after docker ps -a**

```
$ docker rm container id
```

**11. Delete Docker images in local repository**

* Command to see all the local Docker Images
```
$ docker images
```

* Delete Docker Images:
```
$ docker rmi <image name>
```
-> docker run -it -d alpine \bin\sh (run in background)
-> docker run -it alpine \bin\sh (get terminal)
(to execute detached image that is up -> Either by CTRL + P + Q or by opening it in detached mode -d)
-> docker exec -it containter-name \bin\sh
-> docker exec -it cont-name ls

ctrl+p+q -> move back to parent os terminal without exiting and stopping container

start vs exec vs attach
