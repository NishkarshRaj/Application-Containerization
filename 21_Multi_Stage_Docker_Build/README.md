## Multi Stage Docker Builds

multi-stage build functionality is used to make smaller, more optimised images.

The feature is ideal for deploying languages such as Golang as containers. By having multi-stage builds, the first stage can build the Golang binary using a larger Docker image as the base. In the second stage, the newly built binary can be deployed using a much smaller base image. The end result is an optimised Docker Image.

### Creating single Dockerfile for multiple stages

The Multi-Stage feature allows a single Dockerfile to contain multiple stages in order to produce the desired, optimised, Docker Image.

Previously, the problem would have been solved with two Dockerfiles. One file would have the steps to build the binary and artifacts using a development container, the second would be optimised for production and not include the development tools.

By removing development tooling in the production image, you reproduce the attack surface and improve the deployment time.

**Note: Multiple stages means multiple FROM Command, taking advantage of the fact that Docker context is remote and stores the entire history and the image created on build is based on the final context.**

* Clone the Golang HTTP Server

```
$ git clone https://github.com/katacoda/golang-http-server.git
$ cd golang-http-server
```

* Write the Dockerfile called Dockerfile.multi

```dockerfile
# First Stage
FROM golang:1.6-alpine

RUN mkdir /app
ADD . /app/
WORKDIR /app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

# Second Stage
FROM alpine
EXPOSE 80
CMD ["/app"]

# Copy from first stage
COPY --from=0 /app/main /app
```

Using the editor, create a Multi-Stage Dockerfile. The first stage using the Golang SDK to build a binary. The second stage copies the resulting binary into a optimised Docker Image.

### Building Docker Images

Create the desired Docker Image using the build command below.

```
$ docker build -f Dockerfile.multi -t golang-app .
```

The result will be two images. One untagged that was used for the first stage and the second, smaller image, our target image.

`docker images`

If you receive the error, COPY --from=0 /build/out /app/ Unknown flag: from, it means you're running an older version of Docker without the multi-stage support. Step 1 of this scenario upgrades the current Docker version.

![Image](img/.png)

**Note: You can see that Development image containing binary of Docker had 293 MB space but target image is just 12 MB in size**

### Testing successful container launch

The image can be launched and deployed without any changes required.

```
$ docker run -d -p 80:80 golang-app
$ curl localhost
```

## References

[Katacoda Scenario](https://www.katacoda.com/courses/docker/multi-stage-builds)
