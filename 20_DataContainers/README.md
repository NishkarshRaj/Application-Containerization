## Data Containers as alternative to Volumes

Data Containers are containers whose sole responsibility is to be a place to store/manage data.

Like other containers they are managed by the host system. However, they don't run when you perform a docker ps command.

To create a Data Container we first create a container with a well-known name for future reference. We use busybox as the base as it's small and lightweight in case we want to explore and move the container to another host.

When creating the container, we also provide a -v option to define where other containers will be reading/saving data.

* Create a Data Container with mapped volume of container

```
# docker create -v [container volume workspace] --name [container name] [container image]
$ docker create -v /config --name dataContainer busybox
```

* Copy files form local workspace to Data Container

```
# docker cp [files/directory] [container name]:[volume name]
$ docker cp config.conf dataContainer:/config/
```

### Mounting volume from data container to a dependent container

Now our Data Container has our config, we can reference the container when we launch dependent containers requiring the configuration file.

Using the --volumes-from <container> option we can use the mount volumes from other containers inside the container being launched. In this case, we'll launch an Ubuntu container which has reference to our Data Container. When we list the config directory, it will show the files from the attached container

```
# docker run --volumes-from [data container name] [docker image] ls [volume path]
$ docker run --volumes-from dataContainer ubuntu ls /config
```

If a /config directory already existed then, the volumes-from would override and be the directory used. You can map multiple volumes to a container.


### Importing/Exporting Data containers

If we wanted to move the Data Container to another machine then we can export it to a .tar file.

```
$ docker export dataContainer > dataContainer.tar
```

The command `docker import dataContainer.tar` will import the Data Container back into Docker.


## References

[KataCoda Experiments](https://www.katacoda.com/courses/docker/data-containers)
