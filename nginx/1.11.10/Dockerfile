FROM ubuntu:16.04

MAINTAINER Sean Hsu <seanhsu0102@gmail.com>

RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y geoip-database wget git unzip && \
  rm -rf /var/lib/apt/lists/*

ENV NPS_VERSION 1.10.33.4

ENV NGINX 1.11.10

RUN \
    add-apt-repository -y ppa:nginx/stable && \
    apt-get update && \
    apt-get install -y rsyslog libpcre3-dev libpcrecpp0v5 libssl-dev zlib1g-dev libgeoip-dev && \
    rm -rf /var/lib/apt/lists/*

RUN \
  mkdir ~/sources && \
  cd ~/sources && \
    wget http://nginx.org/download/nginx-$NGINX.tar.gz && \
    tar -zxvf nginx-$NGINX.tar.gz && \
    git clone https://bitbucket.org/nginx-goodies/nginx-sticky-module-ng.git && \
    git clone https://github.com/yaoweibin/nginx_upstream_check_module.git && \
    git clone https://github.com/leev/ngx_http_geoip2_module.git && \
  cd nginx-$NGINX && \
  patch -p0 < /root/sources/nginx_upstream_check_module/check_1.11.5+.patch && \
  ./configure \
    --prefix=/etc/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --sbin-path=/usr/sbin/nginx \
    --pid-path=/var/log/nginx/nginx.pid \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --with-http_ssl_module \
    --with-http_gzip_static_module \
    --with-http_stub_status_module \
    --with-http_realip_module \
    --with-http_v2_module \
    --with-http_geoip_module \
    --add-module=/root/sources/nginx-sticky-module-ng \
    --add-module=/root/sources/nginx_upstream_check_module && \
  make && \
  make install && \
  rm -rf ~/sources

RUN useradd nginx

VOLUME ["/var/log/nginx"]

WORKDIR /etc/nginx

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]