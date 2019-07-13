FROM phpdockerio/php73-fpm:latest
WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php7.3-gd php7.3-mysql php7.3-bcmath php-xdebug \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN addgroup --gid 1000 --system dockerhost \
    && adduser --system -uid 1000 --ingroup dockerhost dockerhost \
    && sed -i "/user =/c\user = dockerhost" /etc/php/7.3/fpm/pool.d/www.conf \
    && sed -i "/group =/c\group = dockerhost" /etc/php/7.3/fpm/pool.d/www.conf \
    && echo "zend_extension=\"xdebug.so\"" >> /etc/php/7.3/fpm/php.ini \
    && echo "xdebug.remote_enable = 1" >> /etc/php/7.3/fpm/php.ini \
    && echo "xdebug.remote_port=9001" >> /etc/php/7.3/fpm/php.ini \
    && echo "xdebug.remote_host=${HOSTNAME}" >> /etc/php/7.3/fpm/php.ini \
    && echo "xdebug.remote_connect_back = 1" >> /etc/php/7.3/fpm/php.ini \
    && echo "xdebug.remote_autostart = 1" >> /etc/php/7.3/fpm/php.ini