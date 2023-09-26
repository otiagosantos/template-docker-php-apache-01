# Use a imagem base do Ubuntu 22.10
FROM ubuntu:22.04

# Atualize os pacotes do sistema e instale as dependências necessárias
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    apache2 \
    php \
    php-cli \
    php-json \
    php-xml \
    php-mbstring \
    php-zip \
    php-curl \
    php-mysql \
    php-gd \
    composer \
    php-xdebug

# Habilitar o módulo do Apache para o PHP
# RUN a2enmod php

# Configurar o Xdebug
RUN echo "zend_extension=xdebug.so" > /etc/php/8.1/cli/conf.d/20-xdebug.ini && \
    echo "xdebug.mode=debug" >> /etc/php/8.1/cli/conf.d/20-xdebug.ini && \
    echo "xdebug.start_with_request=yes" >> /etc/php/8.1/cli/conf.d/20-xdebug.ini && \
    echo "xdebug.client_host=host.docker.internal" >> /etc/php/8.1/cli/conf.d/20-xdebug.ini && \
    echo "xdebug.client_port=9000" >> /etc/php/8.1/cli/conf.d/20-xdebug.ini

# Copiar um arquivo de configuração do Apache para ativar a execução de arquivos PHP
COPY apache2.conf /etc/apache2/apache2.conf

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

RUN a2enmod rewrite

RUN apachectl restart

# Expor a porta 80 para o tráfego da web
EXPOSE 80

# Iniciar o Apache em primeiro plano
CMD apache2ctl -D FOREGROUND