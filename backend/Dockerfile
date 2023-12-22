FROM php:8.2-cli

RUN apt-get update && apt-get install -y git curl libpng-dev libonig-dev libxml2-dev zip unzip && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /app/backend
COPY . .
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

EXPOSE 8000
CMD php artisan migrate:fresh --seed && php artisan serve --host=0.0.0.0