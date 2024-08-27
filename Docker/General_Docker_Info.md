# General info

[A practical guide on Docker with projects | Docker Course](https://www.youtube.com/watch?v=rr9cI4u1_88)
[Notion notes](https://www.notion.so/Docker-1861b9434f704a75a62a47b76a220a95?pvs=4)
[Check documentation](https://docs.docker.com/build-cloud/)

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

### Network

_Both applications should live in the same network_

Before connecting to some network we have to create a network using the command:
`$ docker network create --driver bridge some-network`
Otherwise we will get the error: docker: Error response from daemon: network mongo-network not found

**Useful commands**
```shell
# Simple network
--net <NETWORK_NAME>
# List networks
docker network ps
```

## Docker compose

A way to contanirized multiple applications so that they're able to talk with each other

- When creating a docker compose file, docker compose automatically creates a network for all the aplications there

- **Volumes**: Persist data that will be permanent. I'll be mounted up in the container

Check example: `docker-compose.yaml`

```shell
# To execute it 
docker-compose -f docker-compose.yaml up

# Arguments for docker-compose
up      Creates and start containers
down    Remove containers

```

## Docker file

Once you have your docker file:

```shell
# Create the image
docker build -t <NAME> .
            # NAME Usually:
            <DOCKER_ACCOUNT_NAME>/<APP_NAME>:<VERSION>
            # Dot: Defines the docker file in witch the image wll be created. Dot indicates to take it from the current directory

# Create container and run image
docker container run -d -p <PORT_HOST>:<PORT_IMAGE> <IMAGE_NAME>

# Push docker image to repo
docker push <DOCKER_ACCOUNT_NAME>/<APP_NAME>:<VERSION>
```
