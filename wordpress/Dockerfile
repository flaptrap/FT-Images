FROM php:alpine
MAINTAINER FT Networks

WORKDIR /var/www/localhost/

ENV WORDPRESS_DB_HOST localhost
ENV WORDPRESS_DB_USER username
ENV WORDPRESS_DB_PASSWORD password
ENV WORDPRESS_DB_NAME localhost
ENV WORDPRESS_TABLE_PREFIX wp_
ENV WORDPRESS_AUTH_KEY 'put your unique phrase here'
ENV WORDPRESS_SECURE_AUTH_KEY 'put your unique phrase here'
ENV WORDPRESS_LOGGED_IN_KEY 'put your unique phrase here'
ENV WORDPRESS_NONCE_KEY 'put your unique phrase here'
ENV WORDPRESS_AUTH_SALT 'put your unique phrase here'
ENV WORDPRESS_SECURE_AUTH_SALT 'put your unique phrase here'
ENV WORDPRESS_LOGGED_IN_SALT 'put your unique phrase here'
ENV WORDPRESS_NONCE_SALT 'put your unique phrase here'

RUN apk add --no-cache apache2 php7-apache2 php7-common php7-iconv php7-json php7-gd php7-curl php7-xml php7-mysqli php7-imap php7-cgi fcgi php7-pdo php7-pdo_mysql php7-soap php7-xmlrpc php7-posix php7-mcrypt php7-gettext php7-ldap php7-ctype php7-dom php7-session && \
  curl -o wordpress.tar.gz -fSL "https://br.wordpress.org/latest-pt_BR.tar.gz" && \
  rm -r /var/www/localhost/htdocs && \ 
  tar -xzf wordpress.tar.gz -C /var/www/localhost/ && \ 
  mv /var/www/localhost/wordpress /var/www/localhost/htdocs && \ 
  rm wordpress.tar.gz /var/www/localhost/htdocs/wp-config-sample.php /var/www/localhost/htdocs/license.txt /var/www/localhost/htdocs/readme.html && \ 
  chown -R www-data:www-data /var/www/localhost/htdocs/ && \ 
  ln -sf /dev/stdout /var/log/apache2/access.log && ln -sf /dev/stderr /var/log/apache2/error.log

RUN { echo 'opcache.memory_consumption=128'; echo 'opcache.interned_strings_buffer=8'; echo 'opcache.max_accelerated_files=4000'; echo 'opcache.revalidate_freq=2'; echo 'opcache.fast_shutdown=1';} > /usr/local/etc/php/conf.d/opcache-recommended.ini && \ 
  { echo 'error_reporting = E_ERROR | E_WARNING | E_PARSE | E_CORE_ERROR | E_CORE_WARNING | E_COMPILE_ERROR | E_COMPILE_WARNING | E_RECOVERABLE_ERROR'; echo 'display_errors = Off'; echo 'display_startup_errors = Off'; echo 'log_errors = On'; 	echo 'error_log = /dev/stderr'; echo 'log_errors_max_len = 1024'; echo 'ignore_repeated_errors = On'; echo 'ignore_repeated_source = Off'; echo 'html_errors = Off'; } > /usr/local/etc/php/conf.d/error-logging.ini

COPY wp-config.php /var/www/localhost/htdocs/

EXPOSE 80

ENTRYPOINT ["httpd","-D","FOREGROUND"]
