# Docker

## Conceitos Docker

+ Container: Uma imagem em Execução (como se fosse o arquivo.sio em execução)
+ Imagem: É como se fosse o arquivo `.iso` físico

## Comandos Docker

**OBS: execute tudo como sudo**

==> Verificar se o docker está rodando ou não
````
$ systemctl status docker.service

````

==> Subir Docker
````
$ sudo service docker start
````

==> Ver configurações gerais do docker
````
$ docker info
````

==> Verificar as imagens instaladas na máquina.

Lembrando que essas imagens consome bastante espaçço
````
$ docker images
````

Exemplo de saida
````
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ytrec               latest              36a2917e94d0        23 hours ago        1.29GB
<none>              <none>              a6992f2d3cdc        24 hours ago        127MB
python              3.7-slim            64dda927a2fd        10 days ago         120MB
````

==> Deletar imagem (arquivo .iso)

Obs: é necessário saber o ID atraves de `$ docker images`

````
$ docker rmi id_image
````

````
$ sudo docker rmi 36a2917e94d0 -f
````

## List of some Commands

Create a container:
docker run CONTAINER --network NETWORK

Start a stopped container:
docker start CONTAINER_NAME

Stop a running container:
docker stop

List all running containers
docker ps

List all containers including stopped ones
docker ps -a

Inspect the container configuration. For instance network settings and so on:
docker inspect CONTAINER

List all available virtual networks:
docker network ls

Create a new network:
docker network create NETWORK --driver bridge

Connect a running container to a network
docker network connect NETWORK CONTAINER

Disconnect a running container from a network
docker network disconnect NETWORK CONTAINER

Remove a network
docker network rm NETWORK
