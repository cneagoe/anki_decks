# docker

## What is a docker image?

<!-- notecardId: 1761633319056 -->

a template for containers

## What is a docker container?

<!-- notecardId: 1761633319058 -->

a running instance of a image

## How do you start a nginx container?

<!-- notecardId: 1761633319060 -->

```bash
docker run nginx
```

## How do you list all containers running or not?

<!-- notecardId: 1761633319063 -->

```bash
docker ps -a
```

## How do you end a container?

<!-- notecardId: 1761633319066 -->

```bash
docker stop funny_container_name
```

## How do you delete a container?

<!-- notecardId: 1761633319068 -->

```bash
docker rm funny_container_name
```

## How do you see all images?

<!-- notecardId: 1761633319070 -->

```bash
docker images
```

## How do you delete an image?

<!-- notecardId: 1761633319072 -->

```bash
docker rmi nginx
```

## What do you need to ensure before deleting an immage?

<!-- notecardId: 1761633319074 -->

that no containers using the image still exist

## How do you download an immage without also starting a container?

<!-- notecardId: 1761633319077 -->

```bash
docker pull nginx
```

## How do you execute a command on a running container?

<!-- notecardId: 1761633319079 -->

```bash 
docker exec funny_container_name cat /etc/hosts
```

## How can you run a container in the detached mode?

<!-- notecardId: 1761633319081 -->

```bash
docker run -d kodekloud/simple-webapp
```

## How do you attach to a running container?

<!-- notecardId: 1761633319083 -->

```bash 
docker attach container_id_or_funny_name
```

## How do you start a docker container in interactive mode?

<!-- notecardId: 1761633319086 -->

```bash
docker run -it centos bash
```
-i interactive 
-t allocate a pseudo-TTY

## How do you run an older version of an image?

<!-- notecardId: 1761633319088 -->

```bash 
docker run redis:4.0
```

## How do you run a container while mapping port 80 on the host with port 5000 on the container?

<!-- notecardId: 1761633319090 -->

```bash
docker run -p 80:5000 kodekloud/webapp
```

## How do you run a mysql container while bind mounting /opt/datadir on the host to /var/lib/mysql on the container?

<!-- notecardId: 1761633319093 -->

```bash
docker run -v /opt/datadir:/var/lib/mysql mysql
```

## How do you run a mysql container while volume mounting data_volume on the host to /var/lib/mysql on the container?

```bash
docker run -v data_volume:/var/lib/mysql mysql
```

## What is the difference between volume mounting and bind mounting?

<!-- notecardId: 1761633319098 -->

volume mounting mounts a volume from /var/lib/docker/volumes folder
bind mounting mounts a preexisting location

## What is the new alternative to the old -v flag?

<!-- notecardId: 1761633319100 -->

the --mount option

## How would rewrite this cmd with the --mount option "docker run -v /opt/datadir:/var/lib/mysql mysql"?

<!-- notecardId: 1761633319103 -->

```bash
docker run --mount type=bind,source=/opt/datadir,target=/var/lib/mysql mysql
```

## What are some of the most common storage drivers?

<!-- notecardId: 1761633319105 -->

AUFS
ZFS
BTRFS
Device Mapper
Overlay
Overlay2

## Given the output of the ports column : "0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp", which ports are internal and which external?

<!-- notecardId: 1761633319107 -->

3456 80 internal
38080 3456 external

## How do you build an immage and specify the name and author?

<!-- notecardId: 1761633319110 -->

```bash 
docker build Dockerfile -t author/some_app dir/of/Dockerfile
```

## How do you publish an immage from the cli?

<!-- notecardId: 1761633319112 -->

```bash
docker push author/some_app
```

## What command do you run if you want to see teh environment variables set on a running container?

<!-- notecardId: 1761633319115 -->

```bash
docker inspect container-name/id
```

## How do you run a container and set an environment variable?

<!-- notecardId: 1761633319117 -->

```bash 
docker run -p 38282:8080 --name blue-app -e APP_COLOR=blue -d kodekloud/simple-webapp
```

## What is the difference between CMD and ENTRYPOINT?

<!-- notecardId: 1761633319119 -->

at startup, any command specified with the run option will get appended to the ENTRYPOINT, the CMD command will get replaced by any run options.

## How can you set a command that is executed at startup without being explicitly mentioned, with a default value that can be overridden by a run option?

<!-- notecardId: 1761633319122 -->

in the dockerfile
```console
ENTRYPOINT some_command
CMD some_parameter
```
you can then use:
```bash
docker run img_name some_other_parameter
```
at startup the container will run:
```bash
some_command some_other_parameter
```

## What does the FROM command do in a Dockerfile?

<!-- notecardId: 1761633319125 -->

provides a base layer normaly another image for your own

## What does the RUN command do in a Dockerfile?

<!-- notecardId: 1761633319127 -->

runs a command in console of the container

## What does the COPY command do in a Dockerfile?

<!-- notecardId: 1761633319131 -->

copies files or directory from host to image

## What does the ENTRYPOINT command do in a Dockerfile?

<!-- notecardId: 1761633319134 -->

it's usually the command that starts the service you want running on the image

## How can you make two containers aware of each other (depracated)?

<!-- notecardId: 1761633319140 -->

by using the link option
```bash
docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
```

## How many version of docker compose are there?

<!-- notecardId: 1761633319143 -->

version 1 , 2 , 3

## What is the purpose of the services section in the docker compose file?

<!-- notecardId: 1761633319146 -->

to create a dedicated bridged network and attach all containers to that network (links from v1 no longer needed)

## Do you need to explicitly state which version of docker-compose file you are using?

<!-- notecardId: 1761633319148 -->

yes if you are using anything besides v1

## What are the main parts of the docker engine?

<!-- notecardId: 1761633319151 -->

cli, rest api, daemon

## Can the docker cli be run with a remote engine?

<!-- notecardId: 1761633319154 -->

yes

## How are containers isolated inside docker?

<!-- notecardId: 1761633319157 -->

via pid namespaces 
processes runinng inside containers have one pid, 
observed from host they have another pid

## How is resource consumption restricted betweed containers?

<!-- notecardId: 1761633319159 -->

via cgroups
```bash
docker run --cpus=.5 ubuntu
docker run --memory=100m ubuntu
```

## How does docker optimize image build?

<!-- notecardId: 1761633319162 -->

by using a cache system to add only the new image layers

## What happens when you run a container with a volume you haven't created yet?

<!-- notecardId: 1761633319164 -->

docker will automatically create it

## What are the three default docker networks?

<!-- notecardId: 1761633319167 -->

bridge
none 
host

## Deploy an ubuntu container attached to the host network.

<!-- notecardId: 1761633319169 -->

```bash
docker run Ubuntu --network=host
```

## Create a netwokr named custom-isolated with the subnet 182.18.0.0/16 and the bridge driver.

<!-- notecardId: 1761633319172 -->

```bash
docker network create --driver bridge --subnet 182.18.0.0/16 custom isolated
```

## List all docker networks.

<!-- notecardId: 1761633319175 -->

```bash
docker network ls
```

## What is the best way to reach another container on the same network?

<!-- notecardId: 1761633319177 -->

the container name, docker has an internal dns that can map name to ip

## What is the ip adress of the built in docker dns server?

<!-- notecardId: 1761633319179 -->

172.0.0.11

## How do you deploy an image from a private registry?

<!-- notecardId: 1761633319182 -->

```bash 
docker login private-registry.io
docker run private-registry.io/apps/internal-app
```

## How do you deploy a private registry?

<!-- notecardId: 1761633319185 -->

```bash
docker run -d -p 5000:5000 --name registry registry:2
```

## How do you push an image to a local private registry?

<!-- notecardId: 1761633319187 -->

```bash
docker image tag my-image localhost:5000/my-image
docker image push localhost:5000/my-image
```

## How do you check the list of images on a local registry?

<!-- notecardId: 1761633319189 -->

```bash
curl -X GET localhost:5000/v2/_catalog
```

