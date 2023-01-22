FROM php:8.2.2RC1-fpm-alpine3.16 as base

RUN apk update && apk add --no-cache gnupg \
    linux-headers \
    sudo \
    icu-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libsodium-dev \
    libxslt-dev \
    libzip-dev \
    rsync \
    unzip \
    nano \
    bash \
    less \
    iputils \
    iproute2 \
    rabbitmq-c-dev \
    postgresql-dev \
    ;


RUN apk --no-cache add pcre-dev ${PHPIZE_DEPS} \
  && pecl install xdebug amqp \
  && docker-php-ext-enable xdebug \
  && docker-php-ext-enable amqp \
  && apk del pcre-dev ${PHPIZE_DEPS};

RUN apk add libwebp-dev libjpeg-turbo-dev libpng-dev libxpm-dev

RUN docker-php-ext-configure gd --with-webp --with-jpeg --with-xpm --with-freetype

RUN docker-php-ext-install bcmath \
    intl \
    gd \
    opcache \
    soap \
    xsl \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    zip \
    sockets \
    ;

RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
RUN curl -sS https://get.symfony.com/cli/installer | bash \
    && mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

WORKDIR /var/www/

EXPOSE 9000

#CMD ["php"]
#CMD ["symfony", "server:start", "--port=8000"]
