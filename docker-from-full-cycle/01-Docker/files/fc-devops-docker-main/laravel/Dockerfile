FROM php:7.4-cli

WORKDIR /var/www

RUN apt-get update && \ # 
    apt-get install libzip-dev -y && \ # extensao necessaria do php, para doradr o laravel
    docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

#instalar projeto laravle instalado
RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

# Deixar o processo da nossa aplicaçâo rodando
ENTRYPOINT [ "php","laravel/artisan","serve" ] # comando fixo, padrao
CMD [ "--host=0.0.0.0" ]  # esse CMD eu posos mudar pelo cli, já o entry piint nao 

# Eu tenho que passar e o host, porque o laravel-dev rodar no 127.0.1:8000 do container. COmo estou acessando de fora, nâo estou com acesso a esse 127.0.1, entâo tenho que especificar o --host
## Exmplo para subistiuti  esse host por outro
# $ docker run --rm -d --name laravel -p 8001:8001 rafanthx13/larave-re --host=0.0.0.0 --port=8001
## O --host=0.0.0.0 --port=8001 vai substituir o CMD do docker file

# Gera imagem
# docker build -t rafanthx13/laravel-re:latest .

# Executando o nosso container
# $ docker run --rm --name laravel -p 8000:8000 rafanthx13/laravel-re
# SUbimos laravel

#
