FROM php:8-apache
RUN apt-get update -y && apt-get install -y apache2 libmcrypt-dev openssl libzip-dev zip unzip git unixodbc-dev libpng-dev libsodium-dev
RUN pecl install mcrypt mbstring zip

WORKDIR /var/www

COPY ./docker/pma/apache.conf /etc/apache2/sites-enabled/000-default.conf
RUN curl https://files.phpmyadmin.net/phpMyAdmin/5.1.1/phpMyAdmin-5.1.1-english.zip --output pma.zip
RUN unzip pma.zip
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN a2enmod rewrite
RUN docker-php-ext-install pdo pdo_mysql sodium gd zip && docker-php-ext-enable pdo pdo_mysql sodium gd zip

EXPOSE 80
EXPOSE 443
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
