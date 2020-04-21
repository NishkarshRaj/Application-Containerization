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

**Explanation:**

## Docker-compose commands

