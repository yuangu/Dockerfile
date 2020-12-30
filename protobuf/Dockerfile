FROM ubuntu:18.04

LABEL maintainer="lifulinghan@aol.com"

RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
    && apt-get clean \
    && apt-get update 

RUN apt-get install -y --no-install-recommends wget build-essential cmake git \
    && wget --no-check-certificate https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protobuf-all-3.14.0.tar.gz \
    && tar -xvf  protobuf-all-3.14.0.tar.gz \
    && rm -rf protobuf-all-3.14.0.tar.gz \
    && cd protobuf-3.14.0 \
    && ./configure \
    && make \
    && make install \
    && ldconfig \
    && wget --secure-protocol=TLSv1_2 https://sh.rustup.rs -O rustup-init.sh \
    && export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static  \
    && export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup  \
    && sh rustup-init.sh \
    && source $HOME/.cargo/env \
    && cargo install protobuf-codegen  \
    && wget https://npm.taobao.org/mirrors/node/v14.15.3/node-v14.15.3-linux-x64.tar.xz \
    && tar -xvf node-v14.15.3-linux-x64.tar.xz  \
    && rm -rf node-v14.15.3-linux-x64.tar.xz \
    && echo "export PATH=\$PATH:$PWD/node-v14.15.3-linux-x64/bin" > /etc/profile.d/node.sh \
    && source /etc/profile.d/node.sh  \
    && npm install -g protobufjs \
    && pbjs 

RUN apt-get clean  \
    && apt-get -y autoremove  \
    && rm -rf /var/lib/apt/lists/*  \