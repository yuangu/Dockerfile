
FROM ubuntu:18.04

LABEL maintainer="lifulinghan@aol.com"

RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list \
    apt-get -y update && \
    apt-get install -y --no-install-recommends build-essential cmake git  &&\
    apt-get clean &&\
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* 
