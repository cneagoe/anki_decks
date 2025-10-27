# docker

## What is a docker image?

<!-- notecardId: 1759842002180 -->

a template for containers

## What is a docker container?

<!-- notecardId: 1759842002182 -->

a running instance of a image

## How do you start a nginx container?

<!-- notecardId: 1760251420410 -->

```bash
docker run nginx
```

## How do you list all containers running or not?

<!-- notecardId: 1760251420413 -->

```bash
docker ps -a
```

## How do you end a container?

<!-- notecardId: 1760251420415 -->

```bash
docker stop funny_container_name
```

## How do you delete a container?

<!-- notecardId: 1760251420418 -->

```bash
docker rm funny_container_name
```

## How do you see all images?

<!-- notecardId: 1760251420420 -->

```bash
docker images
```

## How do you delete an image?

<!-- notecardId: 1760251420422 -->

```bash
docker rmi nginx
```

## What do you need to ensure before deleting an immage?

<!-- notecardId: 1760251420424 -->

that no containers using the image still exist

## How do you download an immage without also starting a container?

<!-- notecardId: 1760251420426 -->

```bash
docker pull nginx
```

## How do you execute a command on a running container?

<!-- notecardId: 1760251420429 -->

```bash 
docker exec funny_container_name cat /etc/hosts
```

## How can you run a container in the detached mode?

<!-- notecardId: 1760251420432 -->

```bash
docker run -d kodekloud/simple-webapp
```

## How do you attach to a running container?

<!-- notecardId: 1760251420434 -->

```bash 
docker attach container_id_or_funny_name
```

## How do you start a docker container in interactive mode?

<!-- notecardId: 1760932372835 -->

```bash
docker run -it centos bash
```
-i interactive 
-t allocate a pseudo-TTY

## How do you run an older version of an image?

<!-- notecardId: 1760932372838 -->

```bash 
docker run redis:4.0
```

## How do you run a container while mapping port 80 on the host with port 5000 on the container?

<!-- notecardId: 1760932372841 -->

```bash
docker run -p 80:5000 kodekloud/webapp
```

## How do you run a mysql container while maping /opt/datadir on the host to /var/lib/mysql on the container?

<!-- notecardId: 1760932372843 -->

```bash
docker run -v /opt/datadir:/var/lib/mysql mysql
```

## Given the output of the ports column : "0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp", which ports are internal and which external?

<!-- notecardId: 1760932372846 -->

3456 80 internal
38080 3456 external

## How do you build an immage and specify the name and author?

<!-- notecardId: 1760932372848 -->

```bash 
docker build Dockerfile -t author/some_app dir/of/Dockerfile
```

## How do you publish an immage from the cli?

<!-- notecardId: 1760932372851 -->

```bash
docker push author/some_app
```

## What command do you run if you want to see teh environment variables set on a running container?

<!-- notecardId: 1760932372853 -->

```bash
docker inspect container-name/id
```

## How do you run a container and set an environment variable?

<!-- notecardId: 1760932372855 -->

```bash 
docker run -p 38282:8080 --name blue-app -e APP_COLOR=blue -d kodekloud/simple-webapp
```

## What is the difference between CMD and ENTRYPOINT?

<!-- notecardId: 1760932372858 -->

at startup, any command specified with the run option will get appended to the ENTRYPOINT, the CMD command will get replaced by any run options.

## How can you set a command that is executed at startup without being explicitly mentioned, with a default value that can be overridden by a run option?

<!-- notecardId: 1760932372861 -->

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

<!-- notecardId: 1760932372863 -->

provides a base layer normaly another image for your own

## What does the RUN command do in a Dockerfile?

<!-- notecardId: 1760932372865 -->

runs a command in console of the container

## What does the COPY command do in a Dockerfile?

<!-- notecardId: 1760932372868 -->

copies files or directory from host to image

## What does the ENTRYPOINT command do in a Dockerfile?

<!-- notecardId: 1760932372870 -->

it's usually the command that starts the service you want running on the image

## How can you make two containers aware of each other (depracated)?

<!-- notecardId: 1761285851032 -->

by using the link option
```bash
docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
```

## How many version of docker compose are there?

<!-- notecardId: 1761285851038 -->

version 1 , 2 , 3

## What is the purpose of the services section in the docker compose file?

<!-- notecardId: 1761285851041 -->

to create a dedicated bridged network and attach all containers to that network (links from v1 no longer needed)

## Do you need to explicitly state which version of docker-compose file you are using?

<!-- notecardId: 1761285851043 -->

yes if you are using anything besides v1

## What are the main parts of the docker engine?

<!-- notecardId: 1761285851045 -->

cli, rest api, daemon

## Can the docker cli be run with a remote engine?

<!-- notecardId: 1761285851047 -->

yes

## How are containers isolated inside docker?

<!-- notecardId: 1761285851050 -->

via pid namespaces 
processes runinng inside containers have one pid, 
observed from host they have another pid

## How is resource consumption restricted betweed containers?

<!-- notecardId: 1761285851052 -->

via cgroups
```bash
docker run --cpus=.5 ubuntu
docker run --memory=100m ubuntu
```

## How does docker optimize image build?

<!-- notecardId: 1761285851054 -->

by using a cache system to add only the new image layers



