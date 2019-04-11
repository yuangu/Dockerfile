
FROM ubuntu:18.04

MAINTAINER yuangu <lifulinghan@aol.com>

#安装编译环境
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends build-essential autoconf make git &&\
    apt-get install -y --no-install-recommends libssl-dev openssl  libcurl4-openssl-dev curl libbz2-dev libxml2-dev libjpeg-dev libpng-dev libfreetype6-dev libzip-dev

#编译php
RUN curl -o php-7.3.4.tar.xz "https://www.php.net/get/php-7.3.4.tar.xz/from/this/mirror" -L -k && \
    tar -xvJf ./php-7.3.4.tar.xz && \
    cd php-7.3.4 &&\
    ./configure --with-config-file-path=/usr/local/etc/php --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --enable-ftp --with-gd --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-soap --without-pear --with-gettext --disable-fileinfo --enable-maintainer-zts &&\
    make -j "$(nproc)"   && \
    make install &&\
    mkdir /usr/local/etc/php &&\
    cp php.ini-development /usr/local/etc/php/php.ini  &&\
    cd .. &&\
    rm -rf ./php-7.3.4.tar.xz &&\
    rm -rf ./php-7.3.4 

#编译swoole
RUN  curl -o swoole.tar.gz  https://github.com/swoole/swoole-src/archive/v4.3.1.tar.gz -L -k  && \
tar zxvf swoole.tar.gz && \
cd ./swoole-src-4.3.1 && \
phpize && \
./configure \
--enable-openssl  \
--enable-http2  \
--enable-sockets \
--enable-mysqlnd && \
make clean && make && sudo make install &&\
rm -rf swoole-src-4.3.1 &&\
rm -rf swoole.tar.gz


#清理掉不需要的文件
RUN  apt-get clean &&\
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* 