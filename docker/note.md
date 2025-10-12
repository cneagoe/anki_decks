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


