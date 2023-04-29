# FCycle - Docker

## Sumário

+ 0. Código-fonte
  - fc-devops-docker-main.zip

+ 1. Começando do zero
  - 1. Introdução (32min19s)
  - 2. Instalando Docker (05min45s)
  - 3. Conhecendo o WSL 2 (17min04s)
  - 4. Instalando WSL 2 do zero (11min58s)
  - 5. Dicas truques com WSL 2 e Windows Terminal (18min45s)
  - 6. Backup com WSL 2 (09min27s)
  - 7. Integrando Docker com WSL 2 (08min28s)

+ 2. Iniciando com Docker
  - 1. Hello World (08min42s)
  - 2. Executando Ubuntu (09min46s)
  - 3. Publicando portas com nginx (11min50s)
  - 4. Removendo containers (04min55s)
  - 5. Acessando e alterando arquivos de um container (12min22s)
  - 6. Iniciando com bind mounts (11min56s)
  - 7. Trabalhando com volumes (08min21s)

+ 3. Trabalhando com imagens
  - 1. Entendendo imagens e DockerHub (09min22s)
  - 2. Criando primeira imagem com Dockerfile (07min10s)
  - 3. Avançando com Dockerfile (09min15s)
  - 4. ENTRYPOINT vs CMD (09min08s)
  - 5. Docker entrypoint exec (10min29s)
  - 6. Publicando imagem no DockerHub (08min10s)

+ 4. Networks
  - 1. Entendendo tipos de Network (07min43s)
  - 2. Trabalhando com bridge (13min50s)
  - 3. Trabalhando com host (03min37s)
  - 4. Container acessando nossa maquina (05min58s)

+ 5. Colocando em prática
  - 1. Instalando framework em um container (12min49s)
  - 2. Ativando entrypoint e command (17min41s)
  - 3. Criando aplicação Node.js sem o Node (07min37s)
  - 4. Gerando imagem da aplicação Node.js (07min48s)

+ 6. Otimizando imagens
  - 1. Otimização utilizando Multistage Building (12min43s)
  - 2. Nginx como proxy reverso (22min58s)

+ 7. Docker-compose
  - 1. Iniciando com Docker-compose (07min46s)
  - 2. Buildando images com Docker-compose (05min11s)
  - 3. Criando banco de dados MySQL (08min06s)
  - 4. Configurando app node com docker-compose (05min51s)
  - 5. Node vs MySQL (08min42s)
  - 6. Dependência entre containers (11min01s)

+ 9. Desafio
  - 1. Desafio (06min51s)

##  Seção 1 - Começando do Zero

###  1.1 Introdução.mp4 

**O que sâo containers**

Definiçâo  do docker:

Um container é uma padrão de unidade de sofwware que empacato codigo,software e dependenicas, faznedo com que as mesmas sejam executadas rapidamente de forma confiavel independne do ambiente computaicional.

Infelismente isso é uma resposa genérica

Ouvindo a explicaçâo dele:

1 Iplar = NameScpace
Container inicio com a ideia de NameSpace do linux que á a proposta de isolar um procesose e seus sub-pcrocessos de todos os outros. Isso é aplicado ao contianer.

Quando agente afala de container, estamos faladno de procesoss com Namespace. O Conanttaer só enchega somente o próprio proceoss.

Dentro de um Nacpasce há o isolamento de: PID, User, Network, FileSystem.

O que é um container: um processo com subprocesos emulando um SO

2 Pilar = Cgroup = É o que controla os recursos do container
+ O Cgroup é o que limita os recusos, você pode definir por exemplo: memory=500MB, cpu_shares=512
+ Com Cgroup, islamos os recusos usados no container

3 Pilar = File System = OFS = Overlay FIle SYstem
+ O cnontainer tem parte virualizada e parte ficisca, mas, se voce muda alguma coisa, só vai ser alterado na virtualizçaao aquilo que você mudou. Ou seja ELE NÂO FAZ DO ZERO, SE APENAS UMA PEQUENA PART EMUDA.
+ O Container nâo emula todo o okernel do linux/windows. Ele aproveita as já existnete no meu S.O. = Por isso ele é muito leve, **ele não tem todo o sistemaoperacionatal, somente o necessariro, e o resto fica a cargo da maquina que estpa utilziando ofreercer**

**COnceito de Imagem**
+ As imanges sâo um conjunto de camdas, sepraaras que formam uma árvore
+ Exemplo de imagem:
  - Unbuntu
     Bash
     ssh.d
       Myapp:v1
+ Se eu criar uma iamgme igual, mas só como 'MyApp:v1' mudado, a parte do bash/ssh.d/ubnutun SERÃO REAPROVEITADAS. OU seja, agente nâo precisa baixar o ubnutu todo novamente. Agente isola as camads de deprneencias e as reutilziamos em mais de uma imagem.
+ Uma imagme é um conjunto de dependencias encadeadas

img001

**Dockerfile**
+ Arquivo que você descreve a imagem.
+ Agente nâo cria uma imagme do zero, sempre partimaso de outra simagme e nela adicionamos mais dependências.
+ Essa será a 1 linha do docker file, o FROM, baixamos essa imamge e suas dependências
````
FROM: ImageName
````
+ E depois posso personalizar apartir dessa imagme, e expor portas
````
RUN: Comandos ex: apt-get install
EXPOSE: 8000
````

As imamns sâo imutaveis. O que agente conseuqgue alterar no Contianer é umaarea que ele deixa para READ/WRITE, E essa camada nâo altera a imagem.

img002

É possível escrevre nessa área de READ/WRITE, e salavar, fazendo um commit. Aí é entâo gerado uma nova imagem, numa nova versão.

Onde fica as imagesn? em 'IMAGE REGISTRY' 

img003

**O que é então o Docker**

É a junçâo de tudo isso numa coisa só:

img004


###  1.2 -  Instalando Docker e aulas seguintes

Docker foi feito apra rodar no linux, é nele que ele tem todo o pontencial, e é fácil de colcoar nele.

Para Windows/Mac há o 'Docker Desktop' que gera uma psudo-aquina-vitual lnux que ai sim roda DOcker

NO windows vocÊ pode usar o WSL, que é um sub-sistema que opera lniux. Nâo é um amáquina vitrual mas serve para rodar linux e tentar o docker.

**BUSQUE INTALAR CORRETAMENTE O DOCKER NAS UAALS NO LUIS**

**Aulas 3 À 7 sâo auals ensinnado como por o WSL2 No WIndows**

## 2 - Iniciando com Docker

18:55

### 1. Hello World (08min42s)

Comandos como os do Prompt

Listar Containers ativos
$ docker ps

Executar primeiro container
$ docker run hello-world
+ O que isso faz:
  - Vai buscar a imagem `hello-world:latest`, porque, como você não especificou a versão, ele vai buscar a mais recente.
  - Ele vai ver que não encontra a imagem localmente
  - Ele vai baixar do docker hub
  - ELe vai imprimir uma mensagem inicial, pois o `entry-point` dessa imagme é imprimir algo na tela. Ele exibiu a mensagem e morreu, pois o container era apenas executar e morrer

Lista todos os container ativos e inativos
$ docker ps

````
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
d55cf34cdfc7        hello-world         "docker-entrypoint.s…"   5 minutes ago       Up 5 minutes        8080/tcp            hungry_kapitsa

````

Esse 'NAMES' é um nome random que o docker gera, caso você não por um nome.

### 2. Executando Ubuntu (09min46s)

$ docker run -it ubuntu bash
+ Ele nâo vai achar o `ubuntu` e vai baixar a sua imagem
+ `-it` == `-i -t` => Vai liberar para digitar e perar sobre o container; -i = interrativo, acessa terminal ; -t = tty => libera para agente digitar e rodar comandos
+ ELe vai baixar e entrar no ubnutu

Dnadno docker ps

````
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
e67d3dba2be8        ubuntu              "bash"                   2 minutes ago       Up 2 minutes                            heuristic_perlman
```` 

Você pode dar um docker start ou stop sobre o ID ou o NAME dele

Ex: 
$ docker start heuristic_perlman

**O CONTAINER É UM PRCESSO, SE VOCÊ PERDE O PROCESSO, DELETA, OU MANDA DAR STOP, ELE PARA**

flag --rm
$ docker run -it --rm ubuntu bash
+ COm a flag --rm , quando sair, vai desativar o procesos do conatninter. Se nâo faz isso, quando voce entra no contianer, vai subir e deixar ele subido lá. Assim vai remover qunado sair do modo interativo

### 3. Publicando portas com nginx (11min50s)

O nome se fal //En.gin.néks = significa motor x em ingles e ele funciona coomo um servidor web

$ docker run nginx
+ voce  manda um `run`, ele vai procurar localmente, s enao achar, vai baixar
+ O terminal vai ficar parado, e se voce der um docker ps vai ver que ele libera a porta 80, pois a porta 80 é para servidor web
+ Se você tentar entrar em `localhost:80` vai dar erro. Porque?
  - **O CONTAINER NÂO É A SUA MÁQUINA. A PORTA 80 ESTÁ ABERTA NO CONTIANER, NÃO NA SUA MÁQUINA. ISSO PORQUE SOMOS O DOCKER HOST, E NÂO ESTAMOS NA MESMA REDE DOCKER**

Para acessar, temos que publciar a porta, linkar uma porta nossa com a porta 80 do container

$ docker run -p 8080:80 nginx
+ Assim, acessar a porta 8080 na nossa maquina será a nosa 80.

flag -d para liberar terminal
$ docker run -d -p 8080:80 nginx
+ o `-d` significa `detatch` significa para desaplocar o processo do temrinal, asism, eu executo e o processo fica rodando em background NÂO TRAVANDO O TERMINAL

### 4. Removendo containers (04min55s)

$ docker rm CONTAINER-ID-OU-NAME
+ Remove a imagem baixada
+ Só é possível remover com rm imagens que nâo estâo ativadas, para rmeover forçado, use a flag -f para força de vez

$ docker rm -f CONTAINER-ID-OU-NAME 

### 5. Acessando e alterando arquivos de um container (12min22s)

$ docker run -d--name nginx nginx
+ Usamos a flag `--name` para por um nome no container `nginx` se nÂo, fica sendo um nome bizarro

Podemos acessar o container enqunato ele está sendo executado. Para isso usamos `docker exec`

$ docker exec nginx ls
+ Roda comando `ls` no CONTAINER\_ID/NAME `nginx`

Para entrar dentro e xecutar o bash preciso executar o `bash` e a flag `-it`

$ docker exec -it nginx bash
+ vamos acessar a pasta onde fica hospedado o arquivo inicial do ngnix `cd /usr/share/nginx/html/`
+ Tem o arquivo `index.html`
  - Para editra é possivel baixar o vim/nano
  - apt-get vim/nano
+ O vim é semelahnte ao nano, só que meio chatinho
  - VOce entra no arquivo e tem que aperta `i` para entrar no modo de ediçâo
  - Para salvar, tem que sair do modo escrita `ESC` e digitar `:w` e `ENTER`
+ Lembre-se: **A IMAGEM É IMUTÁVEL**. Então, se você matar o processo ou mesmo a imagme, toda a alteração no index.html como o `apt-get update` e `apt-get install nano` **SERÃO PERTIDOS**
+ Par amanter coisa, precisamos usar **VOLUME**

### 6. Iniciando com bind mounts (11min56s)

Bind Mount = Montar volume => É linkar pasta do meu computador como pasta do meu container

$ docker run -d --name ngins -p 8080:80 -v ~/Projects/fullcycle2/docker/html:/usr/share/nginx/html
+ Usamos a flag `-v`
+ VOcê linka a pasta `/Projects/fullcycle2/docker/html` à pasta do container `/usr/share/nginx/html`. Tudo que fizer na sua apsta será refletido no container. E como é sua pasta, tudo que fizer ali será salvo. 

Hoje em dia, a melhor forma é usar a flag `--mount` para faer essa mapeamento

$ docker run -d --name nginx -p 8080:80 --mount type=bind,source="$(pwd)"/html,target=/usr/share/nginx/html nginx

UMa difenrea entre esse comandos é que: 
O `-v` cria pastas e o `--mount` nâo. Isos torna a execuçâo do `--mount` masi segura, pois se você passa rum caminho errado, ele vai acusar erro, enquanto que o -v vai criar pastas loucamente

### 7. Trabalhando com volumes (08min21s)

ATÉ AGORA NÂO ESTAVAMOS TRABALHANDO COM VOLUMES, APENAS ESTAVMAOS FAZENDO UM BIND

$ docker volume
+ Lista os comandos que envolve 'volumes'

$ docker volumes ls
+ lista volumes
+ volumes tem  `DRIVER` e  `VOLUME_NAME`
  -DRIVE para nos, será sempre local, pois é mais asim que vamos trabalhar, com os dados localmente

Criar volumes
$ docker volume create nome_volume 
+ Vai criar volume, esse volumes **NÂO É ONDE SE ESTÁ** É numa pasta interna dos arquivos do docker

$ docker volume inspect  nome_volume
+ Vai listar em json dados do meu volumes criado, indicando o caminho dele
````sh
[
    {
        "CreatedAt": "2023-02-18T19:54:14-03:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/media/rhavel/7A60E25D60E21F9D/docker/volumes/nome_volume/_data",
        "Name": "nome_volume",
        "Options": {},
        "Scope": "local"
    }
]
````

Agora, podemos referenciar esse volume ao invez de passar todo um pwd

$ docker run --name nginx -d --mount type=volume,source=meu_volume,target=/app nginx
+ Linka volume, ao invez de binding que fizmeos antes

OBS: O volume pode ser compartilhado entre outros containers docker

$ docker volume prune
+ Remove todos os arquivos dentro de todos os volumes
+ Isso pode ser util pois, se vocÊ estiver usando arquivos de terceiros, pode acontecer de seu volume encher demais e você nâo entender porque etá tão cheio

## Seção 3 - Trabalhando com imagens

### 1. Entendendo imagens e DockerHub (09min22s)

As imagens que estamos trabalhnado até agora sâo encontradas no site [https://hub.docker.com/](https://hub.docker.com/)

Lá você pode pegar versões difenretes, exemplo, para o nginx existe tags como `nginx:stable-perl`. 

Há vários nomes que apontam para uma mesma imagem. Exemplo no site https://hub.docker.com/_/nginx a latestes pode ter outros nomes que singificam a mesma coisa: \[1.23.3, mainline, 1, 1.23, latest\].
+ e voce fizer `docker pull nginx:mainline` nao vai baixar nada poisjá foi baixada.
+ agora se fizer de outra versâo tipo `docker pull nginx:1.22.1-alpine-perl` aí, avai baixar mesmo.

**Docker hub nâo é o unico DOCKER REGISTRY**
+ Amazon, Azure e o GCP tem os seus proprios DOCKER REGISTRY, que vocÊ usa par amandar coisa privadas para serem executadas em suas clouds.

$ docker images
+ Lista todas as imagesn já baixadas eseus tamanhos

````
REPOSITORY          TAG                  IMAGE ID            CREATED             SIZE
bitnami/laravel     10                   09bb82274b4b        3 days ago          636MB
bitnami/laravel     latest               09bb82274b4b        3 days ago          636MB
nginx               1.22.1-alpine-perl   6d316606ac87        7 days ago          58.5MB
node                16                   b22f8aab05da        7 days ago          910MB
node                lts                  451d8f004bba        7 days ago          996MB
nginx               1.23.3               3f8a00f137a0        9 days ago          142MB
nginx               latest               3f8a00f137a0        9 days ago          142MB
nginx               mainline             3f8a00f137a0        9 days ago          142MB
mysql               8.0                  57da161f45ac        10 days ago         517MB
mysql               5.7                  be16cf2d832a        2 weeks ago         455MB
bitnami/laravel     9                    d0fb6b00d5ce        3 weeks ago         634MB
bitnami/mariadb     10.6                 df2fa2564520        3 weeks ago         338MB
ubuntu              latest               58db3edaf2be        3 weeks ago         77.8MB
hello-world         latest               4653513a6922        2 months ago        264MB
<none>              <none>               aea200091f5d        2 months ago        275MB
node                17-alpine            57488723f087        8 months ago        168MB
<none>              <none>               a6992f2d3cdc        14 months ago       127MB
python              3.7-slim             64dda927a2fd        14 months ago       120MB
````

remover imagem
$ docker rmi php:latest
+ **É IMPORTNATE VOCê ESPECIFICAR A TAG, QUANDO PRECISAR PEGA ALGO ESPECÍFICO**

### 2. Criando primeira imagem com Dockerfile (07min10s)

Vamos criar nosssa próprias imagens.

`Dockerfile`

Lmebra que teinhamso um nginx que nâo tinha o nano já instalado.

**NÃO SERIA BOM TER O nginx mas ját er dentro dele esse `nanp`**

Isos é possivle se criamos o nosso proprio `Dockerfile`

Observeçaoes:
+ Sempre parto de uma imgamge já existente
+ Usamos a flag `-y` para nâo parar o prompt e perguntar se quermeos baixar ou nao, colocamos para baixar direto

````
FROM nginx:latest

RUN apt-get update
RUN apt-get install nano -y
````

Como criar minha imagme docker

$ docker build -t rafanthx13/nginx-modify:latest .
+ colocamos um`.` no final para especificar que é pra ser na pasta em que estou atualmente

Deve entâo criar a imagem localmente e você já pode subir esse contianer 

**VOCE PRECISA CRIAR UMA CONTA NO DOCKER HUB**

### 3. Avançando com Dockerfile (09min15s)

Mais comandos para usar dentro do `Dockerfile`

+ WORKDIR
  - `WORKDIR /the/folder/` : Voce especifica a pasta raiz ao entrar no container, e onde vocÊ vai trabalhar. ELe também criar todo o caminho

````
# Imagem base
FROM nginx:latest

# Definido a riaz do container
WORKINDIR /app

RUN apt-get update && \
    apt-get install vim -y

# Copiar arquivos do meu local para esse container
# Se qualquer pessoa usar a minha imagme, o arquivo index.html interno do container será o que eu acebi de enviar
COPY html/ /usr/share/nginx/html
````

### 4. ENTRYPOINT vs CMD (09min08s)

O Dockerfile deve terminar, em geral, com um comando sendo executado


$ docker rm $(docker ps -a -q) -f
+ ESSE COMANDO É MUITO BOM
+ O que ele faz: remove forçado, todos os containers ativos ou inativos
+ Para pegar só os ativos use sem o -a

**CMD**

No dockerfile podemos por

````
CMD ["echo", "Hello World"]
````

Ao invés disos, podemos também colcoar

$ docker run --rm rafanthx13/nginx-modify:latest echo "oi"
+ Esse `echo "oi` vai substituir o `CMD` defindo no `Dockerfile`

**ENTRY POINT**

Imagine a seguinte imagme
````
FROM ubuntu:latest

ENTRYPOINT ["echo", "Hello"]

CMD ["WORLD"]
````

Se executamos o seguinte comando

$ docker run --rm rafanthx13/hello X
+ Vai mostrar `Hello X` 
$ docker run --rm rafanthx13/hello
+ Vai mostrar `Hello World` 

**O ENTRY PONT É SEMPRE UM COMANDO FIXO, E O CMD É UM APRAMETRO DO MEU ENTRY PONT**

Resumo: Entry Point e CMD sâ executados, mas, se eu passar algum arqumneto, vai susbtituir o CMD mas o Entry point vai sainda rodars

### 5. Docker entrypoint exec (10min29s)

$ docker run --rm -it nginx bash
+ O que esse comando faz
+ Vai roda ro container nginx; Vai executar o bash de modo interativo; Ao sair, o container será parado

+ A amioria dos DOCKERIFEL especificam um arquivo chamado `docker-entrypoint.sh` que sempre está no `ENTRYPONT`. 
+ Nele costuma ter mais umas configuraçoes para serem feitas no container. E no final costuma ter `exec "$@` que serve para EXECUTAR como bash tudp que o usuário digitarr de foma separada. Por isos consigmos dar um bash no nginx e enttar no contianer.
  - QUando agente dar `docker run --rm -it nginx bash` o comando bash substitui o CMD original (que seria apra subir o contianer) e esse docker-entrypoint permite que seja executdado como algo difenret eod conteudo que tme dentor do entry-point


### 6. Publicando imagem no DockerHub (08min10s)

Vamos publicar a seguinte DOckerfile

````
FROM nginx:latest

COPY html /usr/share/nginx/html

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
````
OBS:
+ O docker-entrypoint.sh vem da iamgem original do `ngins:latest`
+ O CMD é apra executar o gninx configurado no `nginx:latest`
+ É a mesma coisa que o ngins:lates, mas, com o copy dos nosso sarquivos

$ docker build -t rafanthx13/primeiro-container .
+ **POr defualt, via colcoar a tag `latest`**
+ VocÊ tem que criar com user\_name/container\_name pois serm o user_aname, vocÊ nao publica no docker hub

Voce tem que logar no prompt do dcker

$ docker login

e depois faze ro push da iamgem já buildada localmente na sua máquina

$ docker push rafanthx13/primeiro-container
 Ai sim vai subir no dockerhub

**OBS: O DOCKER HUB DELETA IMAGENS QUE NÂO SAO BAIXADADS POR MAIS DE 9 DIAS, ENTOA, DE TEMPOS EM TEMPOS FAÇA UM PULL DEA IMAGE, OU FAÇA PAGO**


## 4. Networks

### 1. Entendendo tipos de Network (07min43s)

O Docker cria uma rede interna, que permite um container se conectar com outro, como conectar um laravel com um mysql.

Tipos de Network
+ `brdige`: É a rede default, é o que se usa para um container se conectar com outro
+ `host`: ELa mescla minha rede com a rede do container do a rede `host`. Permite que minha máquina acesse o container sem ter que fazer o `EXPOSE` da porta.
+ `overlay`: Não é um formato muito comun. Serve para conectar container docker **EM MÁQUINAS DIFERNETES**. Usado em conjunto com dockre swarm.
+ `maclan`: Tipo muinto incomun
+ `none`: Especifica que meu container nâo tem rede nehuma

Os formataos que el já utilizou:
+ brige é o mais comun de usar; host algumas verses e o overlay pra trabalhar com o docker-sawn

### 2. Trabalhando com bridge (13min50s)

$ docker newtork
+ lista comandos do network
````
Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks
````

$ docker run -d -it --name ubuntu1 bash
$ docker run -d -it --name ubuntu2 bash

docker network inspect bridge

````
[
    {
        "Name": "bridge",
        "Id": "e6fb8b95038d17a172bd348c561f48ce2dc682e65dc33665cbd742566523353f",
        "Created": "2023-02-19T09:56:34.370195443-03:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "1699dac8f29082cd6964058c660736f131cdd83acd27f6eff4fd97b5b723fa06": {
                "Name": "ubuntu2",
                "EndpointID": "b5b7eb1eef859dee42a4efa5cecee5cd7fb2435e2e0a72d6ce847801dc5300b2",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            },
            "cfd5b4649655747f4924fd83342ef2e9518eb03b0fb1d927dc31cd3d55b7dcdb": {
                "Name": "ubuntu1",
                "EndpointID": "e3d386744eb1559126f58ad2749dcf8d37bb9034217ebb7d85e181e080d4a48b",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
````

Veja que na parte de contianer tem o unbutun1 e unubu2, ou seja, estao na mesma rede

Vamos entrar no container
$ docker attach ubuntu1
+ O attacha é uma outra forma mais fácil de entrar com bash no contianer
+ EU posso pegar o ip do ubuntu 2 e pingar nele normalmente, mas tneho que passar todo o endereço IP tipo 172.56.0

Remova eses container

$ docker rm ubuntu1
$ docker rm ubuntu2

Vou criar uma rede

$ docker network create --driver bridge minha_rede

Depois vou subit os contianer docker colocando essa rede

$ docker run -dit --name ubuntu1 --network minha_rede bash
$ docker run -dit --name ubuntu2 --network minha_rede bash

E como estao na mesma rede, posso fazer o ping apaneas passando o name.

$ docker exec -it ubuntu1 bash
ou 
$ docker attach ubuntu1

Em segudina executo o comando do ping e deve funcionar (funcionou perfeitamente)

\# ping ubuntu2

Use ipp addr show para mostra o ip dentro do bash (é um comando linux)

$ docker network connect minha_rede ubuntu3
+ POdmeos tamém cnectar um contianer a uma rede mesmo depois de criado

e ai verifica

$ docker network inspect minha_rede

### 3. Trabalhando com host (03min37s)

O Docker foi feito para rodar no linux. Assim, a rede `host` só funciona no linux e no WSL2 que são kernels linux de verder. Nâo tem ocmo funcionar no MacOS

$ docker run --rm -d --name nginx --network host nginx
+ Vai juntar as potras do contianer com o seu localhost imediatemnte. 
+ Rede host funciona no Linux e no WSL2

### 4. Container acessando nossa maquina (05min58s)

Como o container docker acessa a prota da minha máquina?

1 - Vou subir o php na minha máquina
$ php -S 0.0.0.0:8000

2 - Subindino o ubuntu no docker
$ docker run --rm -it --name ubuntu ubuntu bash

Dentro do Container
$ apt-get update
$ apt-get install curl -y

Acessando com curl:

$ curl http://host.docker.internal:8080
+ **FUNCIONA**

## Seção 4 - Colocando em prática

### 1. Instalando framework em um container (12min49s) e 2. Ativando entrypoint e command (17min41s)

Vamos aprender a empcatar um frameworks, no caso, será o Laravel. Ele esoclheo php com laravel.

Vamos pegar o `laravel:7.4-cli`

$ docker run -it --name php php:7.4-cli bash

Acessar logs

$ docker logs CONTAINER\_ID\_OU\_NAME 

### 3. Criando aplicação Node.js sem o Node (07min37s)

Nas 2 seçoes anteirores, eu rodieo o laravle fechado. mas

E SE EU QUISER DESENVOLVER EM UMA LINGUAGME/FRAMEWORK SEM PRECISDAR BAIXAR NA MINHA MAQUINA, USANDO O CONTAINER DOCKER, É ISSO QUE VAMOS FAZER COM O NODE.

VOu prograrma NOde sem ter o NOde na minha máquina

$ docker run --rm -it -v $(pwd)/:/user/src/app -p 3000:3000 node:15 bash
Descrevendo esse comando:
+ run = Executar o conainter
+ --rm = Quando sair do comando, vai dar stop no conatienr docker
+ -v $(pwd)/:/user/src/app = Esse $pwd só funciona no linux, eu estou especificando o path atual de onde estou, apr amapear o volume
+ -p 3000:3000 = bind de portas do container par ao meu klocalhost
+ node:15 = O penultimo é a imagme a ser baixada do dockerhub bash = o comando que vai ser rodado

````
$ docker run --rm -it -v $(pwd)/:/usr/src/app -p 3000:3000 node:15 bash
Unable to find image 'node:15' locally
15: Pulling from library/node
bfde2ec33fbc: Pull complete 
787f5e2f1047: Pull complete 
7b6173a10eb8: Pull complete 
dc05be471d51: Pull complete 
55fab5cadd3c: Pull complete 
bd821d20ef8c: Pull complete 
6041b69671c6: Pull complete 
989c5d2d2313: Pull complete 
4b57d41e8391: Pull complete 
Digest: sha256:608bba799613b1ebf754034ae008849ba51e88b23271412427b76d60ae0d0627
Status: Downloaded newer image for node:15
root@680bc31225e4:/# 
````

Como mapeiei o volume, tudo que fizer dentro do bash, tudo quebaixar, vai criar na minha áquina

container: $ cd /usr/src/app
container: $ touch oi
container: $ npm init -y
container: $ npm install express --save
container: $ touch index.js
container: $ apt-get update
container: $ apt-get install nano
container: $ nano index.js

````
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req,res) => {
    res.send('<h1>Full Cycle</h1>')
})

app.listen(port, ()=> {
    console.log('Rodando na porta ' + port)
})
````

container: $ node index.js

E asism, eu posos acessar o locakhost:300 vai acessar meu node

**ASISM, EU POSSO PROGRAMAR SEM TER INSTALADO ALGO NA  MINHA MAQUIAN DIRETAMENTE**S

### 4. Gerando imagem da aplicação Node.js (07min48s)

Agora vamos pegar os passos que fizemos para criar o nosos programa anterior

````
FROM node:15

WORKDIR /usr/src/app

COPY . . # ESSE COMANDO É ULTRA IMPROANTE, SERVE PARA EMPCATORA TODOS OS ARQUIVOS ATULAMENTE E COLOCAR NA MINHA IMAGME

EXPOSE 3000

CMD ["node","index.js"]
````

$ docker build -t rafanthx13/hello-express .

E depois, você pode acessar normalmente

**ESSE `COPY . .` é ultra imporatten. geralmente colocamos ele no `DOckerfile.prod` e nâo colocamos no `Dockerfile`, para assim separa o de produaçao (que precisa ataulziar os arquvios) e o prod normal, de `dev` que não precisa**

$ docker build -t rafanthx13/hello-express node/ -f node/Dockerfile.prod

Aí vai gerar a imagem de produção.


## Seçâo 5 - Otimizando imagens

### 5.1. Otimização utilizando Multistage Building (12min43s)

Vamo gerar uma iamgme em produçao par ao laravel mas bem mais enxuta. 

Vamos usar também 2 contianers: vamos usar o 'nginx' para faer o proxy-reverso. Assim as requisiçoes vao bater no nginx e ele vai pegar os dados do php em outro container.

Vamos também rodar o php no modo fastCgi.

**vamos usar o alpine-linux, que nâo tem nem esmo o apt-get**

Para fica rmelhor, vamos também fazer o build em múltiplas etapas

**IMAGEM ORIGINAL**

````
FROM php:7.4-cli

WORKDIR /var/www

RUN apt-get update && \
    apt-get install libzip-dev -y && \
    docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

ENTRYPOINT [ "php","laravel/artisan","serve" ]
CMD [ "--host=0.0.0.0" ]

````
Consideraçôes
+ 
FPM (effing package manager)
+ 

````
FROM php:7.4-cli AS builder

WORKDIR /var/www

RUN apt-get update && \
    apt-get install libzip-dev -y && \
    docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

FROM php:7.4-fpm-alpine # outra etapa

WORKDIR /var/www 

RUN rm -rf /var/www/html # vamos deletar a pasta html que fica por padrao nela

COPY --from=builder /var/www/laravel . # vamos copiar os arquivos da etapa anterior

RUN chown -R www-data:www-data /var/www # Etamos trocando o dono desses sqruivos, para poder alterar esses arquivos depois

EXPOSE 9000 # porta default do fpm

CMD [ "php-fpm" ] # proggaram que vai eexcutar o php
````

$ docker build -t rafanthx13/laravel:prod . -f Dockerfile.prod

+ o `.` er prara eespecifica o diretorio onde esta o arquivo
+ O `-f` é para especificar o dockerfile, caos tiver mais de um
+ `-t` significa tag, é o nooe do continaer + a tag

Ver se criou a imagme

$ docker images | grep laravel

### 5.2. Nginx como proxy reverso (22min58s)

Vamos subir o gninx para ser o proxy reverso. As requisiçoes vao bater nele e depois vai chamar o php de outro contianer

Vamos usar as configuraçêso do arquivo `nginx.conf` para o onsso nginx

````
FROM nginx:1.15.0-alpine

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d

RUN mkdir /var/www/html -p && touch /var/www/html/index.php
````

build imagem  do dockerfile de produçao

$ docker build -t rafanthx13/nginx:prod . -f Dockerfile.prod

**Vamos agora ligar o laravle e o nginx**

Criar rede

$ docker network create laravel

$ docker run -d --network laravel --name
 laravel rafanthx13/laravel:prod

agora vamos fazer o nginx traalhar

$ docker run -d --network laravel --name nginx -p 8080:80 rafanthx13/nginx:prod

Devo entâo criar um link simbólio no dockerfile do laravel

RUN ln -s public html # link simboloico: É uma forma de fazer atalaho no linux/mac, estou criando um link simbolico, apra quando o nginx acessar o html ele ir e acessar o public do laravel.

O meu nâo deu muito scerto esse negócio do nginx com alravel, mas nâo tem problema



