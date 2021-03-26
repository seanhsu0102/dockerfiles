FROM seanhsu0102/ubuntu:20.04

MAINTAINER Sean Hsu <seanhsu0102@gmail.com>

RUN add-apt-repository ppa:deadsnakes/ppa &&\
    apt-get update && \
    apt-get install -Vy \
    -o APT::Install-Recommends=false -o APT::Install-Suggests=false \
    python3.7 &&\
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

COPY get-pip.py /tmp
RUN /usr/bin/python3.7 /tmp/get-pip.py

CMD ["/usr/bin/python3.7"]