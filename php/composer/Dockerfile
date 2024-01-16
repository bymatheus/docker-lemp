ARG PHP_MAIN_VERSION
ARG PHP_MAIN_INTERPRETER

# Escolher uma imagem base do PHP 8.1
FROM php:${PHP_MAIN_VERSION}-${PHP_MAIN_INTERPRETER}

ARG PATH_CONTAINER

# Instalar dependências necessárias para o Composer e extensões PHP
RUN apt-get update && apt-get install -y \
    zip \
    unzip \
    git \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    libicu-dev \
    && docker-php-ext-install zip mbstring xml curl intl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Instalar o Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Adicionar e configurar grupo e usuário
RUN groupadd -g 1000 laravel && \
  useradd -G laravel -g laravel -s /bin/sh -m laravel

# Definir propriedade dos arquivos
RUN chown -R laravel:laravel ${PATH_CONTAINER}

# Definir o diretório de trabalho
WORKDIR ${PATH_CONTAINER}
