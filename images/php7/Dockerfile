FROM chriswayg/apache-php

# Install pre-requisites for Concrete5 & nano for editing conf files
RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive apt-get -y install \
      php-curl \
      php-gd \
      php-mbstring \
      php-mysql \
      php-xml \
      php-zip \
      unzip \
      wget \
      patch \
      nano && \
    apt-get clean && rm -r /var/lib/apt/lists/*

# Copy apache2 conf dir
# Perl script to enable ability to activate 'Pretty URLs' and redirection in .htaccess by 'AllowOverride'
# - it matches a multi-line string and replaces 'None' with 'FileInfo'
RUN perl -i.bak -0pe 's/<Directory \/var\/www\/>\n\tOptions Indexes FollowSymLinks\n\tAllowOverride None/<Directory \/var\/www\/>\n\tOptions Indexes FollowSymLinks\n\tAllowOverride FileInfo/' /etc/apache2/apache2.conf && \
    cp -r /etc/apache2 /usr/local/etc/apache2 && \
    cd /usr/local/src

COPY php.ini /usr/local/etc/php/

VOLUME ["/var/www", , "/var/log/apache2", "/etc/apache2", "/usr/local/etc/php/"]