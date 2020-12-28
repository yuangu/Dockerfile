FROM ubuntu:18.04

MAINTAINER yuangu <lifulinghan@aol.com>


RUN  sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
&& apt-get clean \
&& apt-get udpate \
&& apt-get install -y --no-install-recommends wget build-essential cmake git \
&& wget https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protobuf-all-3.14.0.tar.gz \
&& tar -xvf  protobuf-all-3.14.0.tar.gz
&& cd protobuf-3.14.0
&& ./configure
&& make
&& make install
&& ldconfig