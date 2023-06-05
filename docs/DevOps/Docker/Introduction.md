# Docker

- Docker is an open-source software that enables the creation, distribution, and running of containers.

-  It provides a set of tools and services that simplify the process of building, deploying, and managing applications within containers.


## Containers

- An isolated environment where all our softwares are installed.

- Containers can be saved, backed up and shared to others.

- They are not OS specific.

## Container, Image, Layer

- We build docker image from layers.
- Docker image in execution is called containers.
- Docker image consists of one or more layers that are stacked on top of each other, forming a layered filesystem.
- Layers can be shared across multiple running containers.

For Example: Suppose we need to deploy a django app using docker containers. Now, to run django, we need python and to run python we need a Linux OS. So, the collection of django layer, python layer, and Linux OS layer when they are stacked together is called Docker Image. We build the docker image that consists of multiple layers and when the docker image is in execution, we call this as docker container.

### Some commands

To get the information about how many containers, process are running and many more info.
```
docker info
```

To search for images : docker search [name of software]
```
docker search httpd
```

To pull docker image
```
docker pull httpd
```

To run the downloaded image
```
docker run -t -i httpd
```
-t means to run in terminal mode <br>
-i means to run in interactive mode

To list all the container
```
docker container ls -a
```

To remove container
```
docker container rm a769b3bd28a0
```
where a769b3bd28a0 is the container id.

To list all the docker image
```
docker image ls
```

To remove the docker image
```
docker image rm httpd
```

To run the container whose image is not in the our local system
```
docker container run -d -p 8080:80 --name apacheinstance httpd
```
-d runs the container in the background <br>
-p 8080:80 maps our system 8080 port to the port 80 of the container <br>
--name apacheinstance : it means we are giving the name to this instance <br>
httpd : the name of the docker image

To list the container running
```
docker ps
```

To remove all the container
```
docker container prune
```

To get logs of last 100 line of the container
```
docker container logs --tail 100 apacheinstance
```

To get inside the container
```
docker container exec -it apacheinstance bash
```