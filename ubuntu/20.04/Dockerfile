FROM ubuntu:focal

MAINTAINER Sean Hsu <seanhsu0102@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

RUN apt-get update && \
    apt-get install -Vy \
    curl \
    locales \
    software-properties-common \
    tzdata \
    wget && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8 LC_CTYPE=en_US.UTF-8

ENV LANG=en_US.UTF-8

RUN echo "Asia/Taipei" > /etc/timezone && \
    ln -fs /usr/share/zoneinfo/Asia/Taipei /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

CMD ["/bin/bash"]