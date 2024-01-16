FROM php:8.1.19-fpm-alpine3.18

COPY ./workspace/run.sh /tmp

WORKDIR /var/www/html

ENTRYPOINT ["/tmp/run.sh"]
