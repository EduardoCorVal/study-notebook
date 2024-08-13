# General info

Video -> https://www.youtube.com/watch?v=rr9cI4u1_88
Check documentation -> https://docs.docker.com/build-cloud/

Docker runs application on top of the system *it doesnt include the kernel*

## Images:

You can store and dowload them in [DockerHub](https://hub.docker.com/)
It´s compose of multiple layers

## Container:

Images run inside them

## [Commands](https://docs.docker.com/reference/)

- Download image: 
`docker pull <IMAGE_NAME>`

- List containers:
`docker ps`

- Run container:
`docker run <IMAGE_NAME>`

- See logs from a container:
```shell
docker logs <IMAGE_NAME>
    --details   # Show extra details
    --follow    # Follow log input
    --since     # Show logs since timestamp
    --tail, -n  `all`   # Number of lines to show from the end of the logs
    --timestamps, -t    # Shot timestamps
    --until     # Show logs before time stamp
```
Note: Look at the offical documentation for each command

**Addtional options when running a container**:

```shell
docker run
    # The desired container's name
    --name <NAME YOU WANT> 
    # The env variables that this container will have. Ex:
    -e
        PASSWORD=secretpassword
    # Detach mode. I'll keep running on the background
    -d
    # Establish from what port the contariner be listening
    -p <PORT_HOST>:<PORT_IMAGE>
    <IMAGE_NAME|IMAGE_ID>:<VERSION>    # The app you'll be running
```

**Useful cleaning commands commands**

```shell
# Remove all docker containers
docker container prune
# Remove all stoping container, dangling image and cache
docker system prune
```

## Docker compose

A way to contanirized multiple applications so that they're able to talk with each other.

Both applications should live in the same network

### References

[A practical guide on Docker with projects | Docker Course](https://www.youtube.com/watch?v=rr9cI4u1_88)