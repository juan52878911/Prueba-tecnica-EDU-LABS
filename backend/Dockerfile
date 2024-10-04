FROM php:8.1-fpm

# Instala dependencias
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpq-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    && docker-php-ext-install pdo pdo_pgsql pdo_mysql mbstring exif pcntl bcmath gd sockets

# Instala Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Crea el directorio de la aplicación
WORKDIR /var/www

# Copia el archivo de dependencias y descarga las dependencias de Laravel
COPY composer.json composer.lock ./
RUN composer install --no-dev --optimize-autoloader

# Copia el resto del código
COPY . .

# Cambia los permisos
RUN chown -R www-data:www-data /var/www \
    && chmod -R 755 /var/www

# Expone el puerto 9000 para PHP-FPM
EXPOSE 9000

CMD ["php-fpm"]
