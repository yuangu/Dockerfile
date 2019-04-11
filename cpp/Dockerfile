
FROM ubuntu:18.04

MAINTAINER yuangu <lifulinghan@aol.com>

RUN apt-get -y update && \
    apt-get install -y --no-install-recommends build-essential cmake git  &&\
    apt-get clean &&\
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* 
