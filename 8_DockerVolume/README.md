##  Docker volumes

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

•	Even if we stop the container or delete it, volume is permanent
•	Re-running another docker container of wordpress after removing

$ docker run –it wordpress bash

•	Remapping but can have different directory of container

•	Docker inspect [id]

•	BCD!!!! By inspecting, default mounted volume
	Volume: permanent storage and communication
	Until container attached deleted, cannot delete volume 
	/var/lib/docker/volumes/[volumename]/_data/{}
	Container with full permission -> sudo -s

❖	Display all docker volumes.

	$ docker volume ls

❖	Create another docker volume named "testvol"

	$ docker volume create --name testvol
	$ docker volume ls

❖	Remove docker volume "testvol"

	$ docker volume rm testvol
	
❖ Delete all the Docker Volumes at once

```
$ docker volume prune
```
