FROM php:7.2-apache

# Install dependencies (git, GD Graphics Library, mysqli, ldap)
RUN apt-get update && apt-get install -y \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libldap2-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install -j$(nproc) ldap

# Download app source
RUN git clone https://github.com/TestLinkOpenSourceTRMS/testlink-code.git /var/www/html

# Provide directory structure
RUN mkdir -p /var/testlink/logs && \
    mkdir -p /var/testlink/upload_area && \
    chmod 777 /var/www/html/gui/templates_c /var/testlink/*

# Add custom configuration
COPY config/custom.ini $PHP_INI_DIR/conf.d/

EXPOSE 80