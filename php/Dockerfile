
FROM ubuntu:18.04

LABEL maintainer="lifulinghan@aol.com"

#安装编译环境
RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list &&\
    apt-get -y update && \
    apt-get install -y --no-install-recommends build-essential autoconf make git &&\
    apt-get install -y --no-install-recommends libssl-dev openssl libsqlite3-dev \
    libonig-dev libpq-dev libcurl4-openssl-dev curl libbz2-dev libxml2-dev libjpeg-dev \
    libpng-dev libfreetype6-dev libzip-dev gnupg2 apt-utils

#编译安装php
RUN curl -o php-7.4.14.tar.xz "http://mirrors.sohu.com/php/php-7.4.14.tar.xz" -L -k &&\
    tar -xvJf ./php-7.4.14.tar.xz &&\
    cd php-7.4.14 &&\
    ./configure --with-config-file-path=/usr/local/etc/php --with-config-file-scan-dir=/usr/local/etc/php/conf.d --enable-fpm --with-mysqli --with-pdo-mysql --with-pdo-pgsql  --with-iconv-dir    --with-zlib  --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --enable-ftp  --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc  --enable-soap --without-pear --with-gettext --disable-fileinfo --enable-maintainer-zts &&\
    make -j "$(nproc)"   &&\
    make install &&\
    mkdir /usr/local/etc/php &&\
    mkdir /usr/local/etc/php/conf.d  &&\
    cp php.ini-development /usr/local/etc/php/php.ini  &&\
    mv /usr/local/etc/php-fpm.d/www.conf.default  /usr/local/etc/php-fpm.d/www.conf &&\
    groupadd nobody &&\
    sed 's!=NONE/!=!g'  /usr/local/etc/php-fpm.conf.default | tee /usr/local/etc/php-fpm.conf > /dev/null &&\
    cd .. &&\
    rm -rf ./php-7.4.14.tar.xz &&\
    rm -rf ./php-7.4.14  

RUN echo "deb [arch=amd64] http://nginx.org/packages/mainline/ubuntu/ bionic nginx">>/etc/apt/sources.list  &&\
    echo "deb-src http://nginx.org/packages/mainline/ubuntu/ bionic nginx">>/etc/apt/sources.list  &&\
    curl -o nginx_signing.key "http://nginx.org/keys/nginx_signing.key" -L -k &&\
    apt-key add nginx_signing.key  &&\
    apt-get update &&\
    apt-get install nginx &&\
    rm -rf /etc/nginx/conf.d/default.conf &&\
    mkdir /work && mkdir /work/public &&\
    echo  'server {   \n \
    listen       80;  \n \
    server_name  localhost;  \n \
    root           /work/public; \n \
    location / { \n \
    index index.php index.html index.htm; \n \
    } \n \
    location ~ \.php?.*$  \n \
    {   \n \
    fastcgi_pass   127.0.0.1:9000;  \n \
    fastcgi_param  SCRIPT_FILENAME  /work/public$fastcgi_script_name;  \n \
    include        fastcgi_params;   \n \
    } \n \
    } \n'  >> /etc/nginx/conf.d/php.conf


#清理不需要的缓存
RUN apt-get clean &&\
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* 

STOPSIGNAL SIGQUIT

CMD ["sh", "-c", "php-fpm&&nginx -g \"daemon off;\""]
