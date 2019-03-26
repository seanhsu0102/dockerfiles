FROM seanhsu0102/ubuntu:16.04

MAINTAINER Sean Hsu <seanhsu0102@gmail.com>

RUN apt-get update && \
    apt-get install -Vy \
    -o APT::Install-Recommends=false -o APT::Install-Suggests=false \
    build-essential \
    libffi-dev \
    libssl-dev \
    python-dev \
    python-pip && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN pip install wheel

CMD ["python"]