FROM ubuntu:20.04

ENV DB_CONNECTION mysql
ENV DB_HOST laraveldb
ENV DB_DATABASE laravel
ENV DB_USERNAME myuser
ENV DB_PASSWORD password
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install software-properties-common -y

RUN add-apt-repository ppa:ondrej/php && apt-get install -y \
    php8.2 \
    php8.2-fpm \
    php8.2-mbstring \
    php8.2-tokenizer \
    php8.2-gd \
    php8.2-xml \
    php8.2-bcmath \
    php8.2-intl \
    php8.2-curl \
    php8.2-simplexml \
    php8.2-dom \
    php8.2-zip \
    php8.2-mysql \
    npm \
    mysql-server \
    nodejs \
    curl \
    git

RUN git clone https://github.com/laravelio/laravel.io.git
WORKDIR /laravel.io

RUN npm install -g n && n latest
RUN npm i vite
RUN npm run build
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"

RUN mv composer.phar /usr/local/bin/composer

RUN composer install

RUN cp .env.example .env
RUN sed -i 's/DB_DATABASE=laravel/DB_DATABASE=${DB_DATABASE}/g' .env
RUN sed -i 's/DB_USERNAME=root/DB_USERNAME=${DB_USERNAME}/g' .env
RUN sed -i 's/DB_PASSWORD=password/DB_PASSWORD=${DB_PASSWORD}/g' .env

RUN php artisan key:generate
EXPOSE 8000

CMD php artisan migrate && php artisan serve --host=0.0.0.0