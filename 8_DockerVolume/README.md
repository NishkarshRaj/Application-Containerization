##  Docker volumes

**Need:**
1. Permanent Storage
2. Inter container communication by common storage

❖ Create a volume that would be stored permanently on parent OS but controlled by Docker engine

```
$ docker volume create --name [volume name]
$ docker volume ls
```

❖ Run docker container and mount the volume by synchronizing it with a directory in the container.

```
$ docker run -it -v [volume name]:[Absolute path of sync folder] [image name] bash
```
* If path of the sync folder specified does not exists, creates on container launch.
* Docker Volumes are stored at **/var/lib/Docker/volumes**

❖ Make changes in the synchronized folder of the container

```
$ cd [sync folder]	
$ echo “Hello World” >> test.txt
$ exit	
```

**Note: To give root permissions in Docker and Vagrant, use** `$ sudo -s`

❖ Inspecting the default mounted volume:

```
$ docker inspect [Container name or container ID]
```
	
**Note: Until container attached deleted, cannot delete volume** 

**Note: Volume data is stored at** `/var/lib/docker/volumes/[volumename]/_data/{}`

❖ Display all docker volumes.

```
$ docker volume ls
```

❖ Remove docker volume by name or ID

```
$ docker volume rm [volume name or volume ID]
```

❖ Delete all the Docker Volumes at once

```
$ docker volume prune
```
