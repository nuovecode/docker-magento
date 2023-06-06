FROM php:8.1.19-fpm-alpine

ARG DOCKER_IMAGE_FOLDER
ARG GROUP_ID
ARG USER_ID

RUN apk add --upgrade gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so

RUN apk --no-cache --repository https://dl-cdn.alpinelinux.org/alpine/edge/main add \
    icu-libs \
    &&apk --no-cache --repository https://dl-cdn.alpinelinux.org/alpine/edge/community add \
    # Current packages don't exist in other repositories
    libavif \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ --allow-untrusted gnu-libiconv \
    # Packages
    tini \
    php81 \
    php81-dev \
    php81-common \
    php81-gd \
    php81-xmlreader \
    php81-bcmath \
    php81-ctype \
    php81-curl \
    php81-exif \
    php81-iconv \
    php81-intl \
    php81-mbstring \
    php81-opcache \
    php81-openssl \
    php81-pcntl \
    php81-phar \
    php81-session \
    php81-xml \
    php81-xsl \
    php81-zip \
    php81-zlib \
    php81-dom \
    php81-fpm \
    php81-sodium \
    php81-tokenizer \
    php81-pdo \
    php81-pdo_mysql \
    php81-simplexml \
    php81-xmlwriter \
    php81-soap \
    php81-sockets \
    php81-fileinfo \
    php81-mysqli \
     # Iconv Fix
    php81-pecl-apcu \
    && ln -sf /usr/bin/php81 /usr/bin/php

# php intl dependencies
RUN apk add icu-dev
RUN apk add icu-libs

# php gd dependencies
RUN apk add jpeg-dev
RUN apk add libpng-dev
RUN apk add freetype-dev

# php soap dependencies
RUN apk add libxml2-dev

# php xsl dependencies
RUN apk add libxslt-dev

# php zip dependencies
RUN apk add libzip-dev

# php oniguruma
RUN apk add oniguruma
RUN apk add oniguruma-dev

RUN docker-php-ext-install pdo_mysql

RUN docker-php-ext-install intl

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

COPY $DOCKER_IMAGE_FOLDER/php-fpm/php.ini /usr/local/etc/php/php.ini

# Git
RUN apk add git

# Composer
RUN apk add composer

RUN addgroup -g $GROUP_ID -S dockeruser

RUN adduser -S -G dockeruser -u $USER_ID -s /bin/ash dockeruser

RUN chown -R dockeruser: /usr/local/etc/php

USER dockeruser

WORKDIR /home/dockeruser/magento

EXPOSE 9000

