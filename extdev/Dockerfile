FROM ubuntu:latest

RUN set -ex \
&& sed -i s@/archive.ubuntu.com/@/mirrors.ustc.edu.cn/@g /etc/apt/sources.list \
&& apt clean \
&& apt update \
&& apt upgrade \
&& apt install -y \
	libzzip-dev \
	libzip-dev \
	libgd-dev \
	libpng-dev \
	libwebp-dev \
	libfreetype6-dev \
	libxslt1-dev \
	libpng-dev \
	libxpm-dev \
	gettext \
	libxslt1-dev \
	libwebp-dev \
	libicu-dev \
	libturbojpeg-dev \
	libxml2-dev \
	libmemcached-dev \
	wget \
	libcurl4 \
	curl \
	gcc \
	autoconf \
	vim \
	less \
	re2c \
	bison \
	net-tools \
	iputils-ping \
#openssl
&& cd ~ \
&& wget -t0 --no-check-certificate https://www.openssl.org/source/openssl-1.1.1d.tar.gz \
&& tar zfvx ./openssl-1.1.1d.tar.gz \
&& cd openssl-1.1.1d \
&& ./config \
&& make -j 4 \
&& make install \
&& cd ~ \
&& rm -rf openssl* \
&& wget -t0 --no-check-certificate -O /usr/local/ssl/cert.pem http://curl.haxx.se/ca/cacert.pem \
#php
&& cd ~ \
&& wget -t0 --no-check-certificate -O ./php73.tar.gz https://www.php.net/distributions/php-7.3.9.tar.gz \
&& tar zfvx ./php73.tar.gz  \
&& mv ./php-7.3.9 ./php \
&& rm -rf php73* \
&& cd ./php \
&& ./configure --with-openssl=/usr/local --enable-debug --with-zlib --with-pdo-mysql=mysqlnd --enable-mysqlnd --with-mysqli=mysqlnd --enable-mbstring --enable-pcntl --enable-bcmath --enable-zip --with-gd=/usr --with-gettext=/usr --with-xsl=/usr --enable-intl --with-webp-dir=/usr --with-jpeg-dir==/usr --with-freetype-dir=/usr --with-xpm-dir=/usr \
&& make -j 4 \
&& make install \
&& cp php.ini-development /usr/local/lib/php.ini \
&& cd ./ext \
#redis
#&& wget  -t0 --no-check-certificate -O ./phpredis.tar.gz  https://github.com/phpredis/phpredis/archive/4.2.0.tar.gz \
#&& tar zfvx ./phpredis.tar.gz \
#&& cd phpredis-* \
#&& phpize  \
#&& ./configure \
#&& make -j 4  \
#&& make install \
#&& sed -i '$a\extension=redis.so' /usr/local/lib/php.ini \
#&& cd .. \
#&& rm -rf php/ext/phpredis* \
#xdebug
#&& wget  -t0 --no-check-certificate -O ./xdebug-2.8.0beta2.tgz  https://xdebug.org/files/xdebug-2.8.0beta2.tgz \
#&& tar zfvx ./xdebug-2.8.0beta2.tgz \
#&& cd xdebug-2.8.0beta2 \
#&& phpize  \
#&& ./configure \
#&& make -j 4  \
#&& make install \
#&& sed -i '$a\zend_extension=xdebug.so' /usr/local/lib/php.ini \
#&& cd .. \
#&& rm -rf php/ext/xdebug* \
#swoole
#&& wget -t0 --no-check-certificate -O ./swoole.tar.gz  https://github.com/swoole/swoole-src/archive/v4.2.9.tar.gz \
#&& tar zfvx ./swoole.tar.gz \
#&& cd swoole-* \
#&& phpize \
#&& ./configure \
#&& make -j 4  \
#&& make install \
#&& sed -i '$a\extension=swoole.so' /usr/local/lib/php.ini \
#&& cd .. \
#&& rm -rf php/ext/swoole* \
#composer
&& cd ~ \
&& php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
&& php composer-setup.php \
&& php -r "unlink('composer-setup.php');" \
&& mv ./composer.phar /usr/local/bin/ \
&& ln -s /usr/local/bin/composer.phar /usr/local/bin/composer \
&& composer self-update \
&& composer global config repo.packagist composer https://mirrors.aliyun.com/composer/ \
&& composer global require phpunit/phpunit -vvv \
&& composer global config --unset repos.packagist \
&& sed -i '$a\export PATH="\$HOME/.composer/vendor/bin:\$PATH"' ~/.bashrc 

WORKDIR /root/php/ext

CMD ["/bin/bash"]

