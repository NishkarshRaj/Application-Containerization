## Creating Private Registry for Docker containers
 
1. Create a private registry on your domain

```
docker run -d -p 5000:5000 \
    -v /root/certs:/certs \
    -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/registry.test.training.katacoda.com.crt \
    -e REGISTRY_HTTP_TLS_KEY=/certs/registry.test.training.katacoda.com.key \
    -v /opt/registry/data:/var/lib/registry \
    --name registry registry:2
```

* Daemon mode - always running in background
* Port mapping
* Certificates must be gathered for the domain. Link in description
* Mount certificates to a certain folder in **registry** container, here **certs/**
* Setup Environment variables in the registry container by using certs that were mounted in previous step.
* Mount **/var/lib/registry** - all the pushed containers would be stored here
* Image used for private registry - **registry:2**

2. Check for secure SSL connection to the registry (Security is implemented using **TLS + Nginx**)

```
$ curl -i https://registry.test.training.katacoda.com:5000/v2/
```

3. Pull an image from DockerHub registry and tag it according to the domain of your registry.

**Note: Generally all images are named as [Image]:[tag] because they are linked with default DockerHub registry. 
General Image names are [Domain name]:[Image name]:tag**

```
$ docker pull redis:alpine 
$ docker tag redis:alpine registry.test.training.katacoda.com:5000/redis:alpine
```

4. Push the images to registry
  
```
$ docker push registry.test.training.katacoda.com:5000/redis:alpine
```

5. Delete the images from local machine

```
$ docker rmi redis:alpine && docker rmi registry.test.training.katacoda.com:5000/redis:alpine
```

6. Pull the image from private registry

```
$ docker pull registry.test.training.katacoda.com:5000/redis:alpine
```

## References

[KataCoda scenario](https://www.katacoda.com/courses/docker-production/launch-private-registry)

[Docker Registry docs 1](https://docs.docker.com/registry/)

[Docker Registry docs 2](https://docs.docker.com/registry/deploying/)

[Generate Certificates for your Registry](letsencrypt.org)
