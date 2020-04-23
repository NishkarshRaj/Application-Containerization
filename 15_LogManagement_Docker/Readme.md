## Managing Log Files

### 1) Standard Logging: JSON Outputting

* Docker Engine keeps a track of the **Standard Error** and **Standard Output** Stream and maintains a log of the same which can be made available to the client using the following command:

```
$ docker logs [container name or ID]
```

### 2) SYSLog
 
By default, the Docker logs are outputting using the json-file logger meaning the output stored in a JSON file on the host. 
This can result in large files filling the disk.
As a result, you can change the log driver to move to a different destination

**Syslog:** Syslog is a widely used standard for message logging. It permits separation of the software that generates messages, the system that stores them, and the software that reports and analyses them.

```
docker run --log-driver=syslog [Image name]
```

* Checking logs of Docker containers whose logs are synced with Syslog driver result in FATA[0000] error. System logs can only be accessed by using the Syslog stream.

### 3) Disable Logging

We can disable logging for some containers that are not very critical but very verbose.

```
$ docker run --log-driver=none [image name]
```

## References

[KataCoda Scenarios](https://katacoda.com/courses/docker/8)
