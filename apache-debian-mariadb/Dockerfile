FROM drupal:8.7-apache

RUN apt-get update && apt-get install -y \
	curl \
	git \
	mysql-client \
	vim \
	wget

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php composer-setup.php && \
	mv composer.phar /usr/local/bin/composer && \
	php -r "unlink('composer-setup.php');"

RUN wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/0.4.2/drush.phar && \
	chmod +x drush.phar && \
	mv drush.phar /usr/local/bin/drush

# Removing Drupal downloaded from official drupal docker image and rm -rf /root/.composer is to remove composer cache

RUN rm -rf /var/www/html/* && rm -rf /root/.composer

COPY apache-drupal.conf /etc/apache2/sites-enabled/000-default.conf

RUN mkdir /app

# Download SM Dev portal code from packagist https://packagist.org/packages/apigee/devportal-kickstart-project
RUN composer create-project apigee/devportal-kickstart-project:8.x-dev /app --no-interaction

RUN mkdir -p /app/config/sync

RUN chown -R www-data:www-data /app/web
