# https://hub.docker.com/_/phpにあるイメージファイルを指定
FROM php:8.2-fpm
COPY php.ini /usr/local/etc/php/

RUN apt-get update \
  && apt-get install -y zlib1g-dev mariadb-client vim libzip-dev \
  && docker-php-ext-install zip pdo_mysql
    
# Composerのインストール & パス通す
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# nodeインストール(aptだとNodejsは古いため、パッケージマネージャの n を使用してインストール)
RUN apt install -y npm \
    && npm install n -g \
    && n stable

# RUN , CMD , ENTRYPOINT , COPY , ADD を実行する時のワーキングディレクトリを指定
WORKDIR /var/www

# Laravelのインストール
# RUN composer create-project --prefer-dist laravel/laravel .