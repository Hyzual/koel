# Koel all-in-one for development
FROM debian:buster

# Install dependencies
RUN apt-get update && \
  apt-get install --yes --no-install-recommends \
    # supervisord will start php-fpm and nginx
    supervisor \
    nginx \
    php-curl \
    php-tokenizer \
    php7.3-bcmath \
    php7.3-common \
    php7.3-fpm \
    php7.3-json \
    php7.3-mbstring \
    php7.3-mysql \
    php7.3-xml \
    php7.3-zip \
    libzip-dev \
    zip \
    ffmpeg \
  && apt-get clean \
  # Remove default nginx configuration
  && rm /etc/nginx/sites-enabled/default \
  # Create php-fpm unix socket directory
  && mkdir /run/php

# Create writable directories for Laravel
RUN install -d --owner=www-data --group=www-data /usr/share/koel/storage/logs \
  && install -d --owner=www-data --group=www-data /usr/share/koel/storage/framework/views \
  && install -d --owner=www-data --group=www-data /usr/share/koel/storage/framework/cache

COPY supervisord.conf /etc/supervisord.conf
COPY nginx.conf /etc/nginx/conf.d/koel.conf

ENV FFMEPG_PATH=/usr/bin/ffmpeg \
    MEDIA_PATH=/music \
    STREAMING_METHOD=x-accel-redirect

WORKDIR /usr/share/koel
VOLUME ["/music", "/usr/share/koel"]
EXPOSE 80
# Run supervisord to handle nginx & fpm
CMD ["supervisord", "-n", "-c", "/etc/supervisord.conf"]
