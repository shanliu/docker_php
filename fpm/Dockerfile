FROM php:7.3-fpm-alpine


RUN set -ex \
#public
&&sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/' /etc/apk/repositories \
&& apk update \
&& apk add --no-cache \
	zlib-dev \
	libzip-dev \
	gd-dev \
	jpeg-dev \
	libwebp-dev \
	freetype-dev \
	libpng-dev \
	gettext-dev \
	libxslt-dev \
	icu-dev \
	libmemcached-dev \
&& docker-php-source extract \
&& wget -O ./phpredis.tar.gz  https://github.com/phpredis/phpredis/archive/4.2.0.tar.gz \
&& tar zfvx ./phpredis.tar.gz \
&& mv phpredis-* /usr/src/php/ext/redis \
&& rm -rf phpredis-* \
#docker-php-ext-configure gd  --with-jpeg-dir=/usr/include/  --with-freetype-dir=/usr/include/
&& docker-php-ext-install \
	sockets \
	bcmath \
	zip \
	mysqli \
	gd \
	pdo_mysql \
	gettext \
	xsl  \
	intl \
	redis \
#fpm
&& wget -O ./yaf.tar.gz  https://github.com/laruence/yaf/archive/yaf-3.0.8.tar.gz \
&& tar zfvx ./yaf.tar.gz \
&& mv yaf-* /usr/src/php/ext/yaf \
&& rm -rf yaf-* \
&& docker-php-ext-install \
	yaf \
#composer
&&php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
&& php -r "if (hash_file('sha384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
&& php composer-setup.php \
&& php -r "unlink('composer-setup.php');" \
&& mv ./composer.phar /usr/local/bin/ \
&& ln -s /usr/local/bin/composer.phar /usr/local/bin/composer \
&& composer config -g secure-http false \
&& composer self-update \
#clear
&& rm -rf /usr/src/php/* \
&& rm -rf /var/cache/apk/* /tmp/* /usr/share/man 

WORKDIR /var/www

CMD ["php-fpm","-F"]