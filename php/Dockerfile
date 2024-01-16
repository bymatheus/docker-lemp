ARG PHP_MAIN_VERSION
ARG PHP_MAIN_INTERPRETER

FROM php:${PHP_MAIN_VERSION}-${PHP_MAIN_INTERPRETER}

ARG PATH_CONTAINER

# Copy configuration files
COPY www.conf /usr/local/etc/php-fpm.d/www.conf
COPY config/custom.ini /usr/local/etc/php/conf.d/custom.ini

# Add and set user/group, create directory, set ownership
RUN groupadd -g 1000 laravel && \
    useradd -G laravel -g laravel -s /bin/sh -m laravel && \
    mkdir -p ${PATH_CONTAINER} && \
    chown laravel:laravel ${PATH_CONTAINER}

# Set working directory
WORKDIR ${PATH_CONTAINER}

# Install dependencies and PHP extensions
RUN apt update && \
    apt-get install -y \
    default-mysql-client \
    zlib1g-dev \
    libzip-dev \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} gd pdo pdo_mysql zip && \
    apt-get clean

RUN rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install zip
