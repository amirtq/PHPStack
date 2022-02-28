FROM php:7.4-apache
RUN apt update && apt install -y nano vim cron systemctl
RUN docker-php-ext-install pdo pdo_mysql && docker-php-ext-enable pdo pdo_mysql
RUN apt update && apt install -y zlib1g-dev libpng-dev && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install gd
RUN a2enmod rewrite && a2enmod ssl && a2enmod proxy_http
#conrtab configuration, the real cron file you need to use is located in ./apache2-and-php/cronjobs
RUN touch /var/log/cron.log
COPY cronhelper /etc/cron.d/cronhelper
RUN chmod 0644 /etc/cron.d/cronhelper
RUN crontab /etc/cron.d/cronhelper
RUN sed -i 's/^exec /service cron start\n\nexec /' /usr/local/bin/apache2-foreground
