FROM vitamin/alpine:3.6
LABEL maintainer="roy<zhushaoqing@ispied.com>"
# persistent / runtime deps
ENV PHPIZE_DEPS \
		autoconf \
		dpkg-dev dpkg \
		file \
		g++ \
		gcc \
		libc-dev \
		make \
		pkgconf \
		re2c
RUN apk add --no-cache --virtual .persistent-deps \
		ca-certificates \
		curl \
		tar \
		xz \
# https://github.com/docker-library/php/issues/494
		libressl

# ensure www-data user exists
RUN set -x \
	&& addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data
# 82 is the standard uid/gid for "www-data" in Alpine
# http://git.alpinelinux.org/cgit/aports/tree/main/apache2/apache2.pre-install?h=v3.3.2
# http://git.alpinelinux.org/cgit/aports/tree/main/lighttpd/lighttpd.pre-install?h=v3.3.2
# http://git.alpinelinux.org/cgit/aports/tree/main/nginx-initscripts/nginx-initscripts.pre-install?h=v3.3.2



# 软件包安装
RUN apk add php7@community \
        php7-fpm@community \
        php7-opcache@community \
        php7-session@community \
        php7-xml@community \
        php7-ctype@community \
        php7-gd@community \
        php7-json@community \
        php7-posix@community \
        php7-curl@community \
        php7-dom@community \
        php7-pdo@community \
        php7-pdo_mysql@community \
        php7-sockets@community \
        php7-zlib@community \
        php7-mcrypt@community \
        php7-mysqli@community \
        php7-sqlite3@community \
        php7-bz2@community \
        php7-phar@community \
        php7-posix@community \
        php7-zip@community \
        php7-calendar@community \
        php7-iconv@community \
        php7-imap@community \
        php7-soap@community \
        php7-dev@community \
        php7-pear@community \
        php7-redis@community \
        php7-mbstring@community \
        php7-xdebug@community \
        php7-exif@community \
        php7-xsl@community \
        php7-ldap@community \
        php7-openssl@community \
        php7-bcmath@community \ 
        php7-xml@community \
        php7-intl@community \
        php7-simplexml@community \
        php7-xmlreader@community \
        php7-xmlwriter@community \
        php7-tokenizer@community


# 从国内镜像安装composer，并配置成默认从国内镜像安装composer包
RUN php -r "readfile('http://install.phpcomposer.com/installer');" | php -- --install-dir=/bin/ --filename=composer
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com
RUN mkdir /apps \ 
        && ln -sf /etc/php7 /etc/php \
        && ln -sf /usr/sbin/php-fpm7 /usr/bin/php-fpm \
        && ln -sf /var/log/php7 /var/log/php \
        && chown -R www-data:www-data /etc/php \
        && chown -R www-data:www-data /var/log/php \
        && chown -R www-data:www-data /etc/php \ 
        && chown -R www-data:www-data /apps \
        && composer self-update
VOLUME /apps

WORKDIR /apps
# 端口号配置
EXPOSE 9000

# User/Group
ENV VITAMIN_USER="vitaminbox" \
	VITAMIN_GROUP="vitaminbox" \
	VITAMIN_UID="1000" \
        VITAMIN_GID="1000"


# 容器命令执行
CMD ["php-fpm","-c","/etc/php/php-fpm.conf"]