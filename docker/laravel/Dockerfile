FROM php:8.1.18-fpm as build-composer
WORKDIR /application
RUN apt-get update && apt-get install -y \
  git \
  zip \
  unzip \
  && curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer


FROM php:8.1.18-fpm
COPY ./src /application
WORKDIR /application
COPY --from=build-composer /usr/local/bin/composer /usr/local/bin/composer
RUN apt-get update && apt-get install -y \
  git \
  zip \
  unzip \
  && composer install
RUN php artisan cache:clear \
  && php artisan config:clear \
  && php artisan route:clear \
  && php artisan view:clear
RUN chown -R www-data:www-data storage
