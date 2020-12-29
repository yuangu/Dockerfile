FROM ubuntu:18.04

LABEL maintainer="lifulinghan@aol.com"

RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
    && apt-get clean \
    && apt-get update \
    && apt-get install -y --no-install-recommends wget build-essential cmake git \
    && wget https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protobuf-all-3.14.0.tar.gz \
    && tar -xvf  protobuf-all-3.14.0.tar.gz \
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
    && cargo install protobuf  \
    && apt-get clean  \
    && apt-get -y autoremove  \
    && rm -rf /var/lib/apt/lists/* 