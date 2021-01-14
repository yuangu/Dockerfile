
FROM ubuntu:18.04

LABEL maintainer="lifulinghan@aol.com"


#安装编译环境
RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
    apt-get -y update && \
    apt-get install -y --no-install-recommends build-essential autoconf make git &&\
    apt-get install -y --no-install-recommends libssl-dev openssl  libcurl4-openssl-dev curl libbz2-dev libxml2-dev libjpeg-dev libpng-dev libfreetype6-dev libzip-dev gnupg2

#编译安装php
RUN curl -o php-7.4.14.tar.xz "https://www.php.net/distributions/php-7.4.14.tar.xz" -L -k && \
    tar -xvJf ./php-7.4.14.tar.xz && \
    cd php-7.4.14 &&\
    ./configure --with-config-file-path=/usr/local/etc/php --with-config-file-scan-dir=/usr/local/etc/php/conf.d --enable-fpm --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --enable-ftp --with-gd --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-soap --without-pear --with-gettext --disable-fileinfo --enable-maintainer-zts &&\
    make -j "$(nproc)"   && \
    make install &&\
    mkdir /usr/local/etc/php &&\
    mkdir /usr/local/etc/php/conf.d  &&\
    cp php.ini-development /usr/local/etc/php/php.ini  &&\    
    cd .. &&\
    rm -rf ./php-7.4.14.tar.xz &&\
    rm -rf ./php-7.4.14  

RUN echo "deb [arch=amd64] http://nginx.org/packages/mainline/ubuntu/ bionic nginx">>/etc/apt/sources.list  && \
    echo "deb-src http://nginx.org/packages/mainline/ubuntu/ bionic nginx">>/etc/apt/sources.list  &&\
    curl -o nginx_signing.key "http://nginx.org/keys/nginx_signing.key" -L -k &&\
    apt-key add nginx_signing.key  &&\
    apt-get update &&\
    apt-get install nginx 



#清理不需要的缓存
RUN apt-get clean &&\
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* 