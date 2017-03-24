FROM ubuntu:xenial
MAINTAINER Bronsoms

ENV DEBIAN_FRONTEND noninteractive
ENV COMPOSER_DISABLE_XDEBUG_WARN 1

RUN PACKAGES_TO_INSTALL="apache2 php7.1 php7.1-intl php7.1-xml composer php7.1-zip php7.1-mbstring libapache2-mod-php7.1 php7.1-curl php7.1-fpm php7.1-mysql unzip" && \
    apt-get update && \
    apt-get install -y software-properties-common && \
    apt-add-repository -y ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y --allow-unauthenticated $PACKAGES_TO_INSTALL && \
    apt-get autoremove -y && \
    apt-get clean && \
    apt-get autoclean

# Enable apache mods.
RUN a2enmod php7.1
RUN a2enmod rewrite

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Expose apache.
EXPOSE 80

# Configure Virtualhost
ADD apache/000-default.conf /etc/apache2/sites-enabled/000-default.conf

# By default start up apache in the foreground, override with /bin/bash for interative.
CMD /usr/sbin/apache2ctl -D FOREGROUND

# Set working dir
WORKDIR /var/www
