FROM centos:7
LABEL maintainer www.xianliru.com
RUN useradd  www -u 1200 -M -s /sbin/nologin
RUN mkdir -p /var/log/nginx
RUN mkdir -p /usr/local/nginx/conf/conf.d
RUN mkdir -p /usr/local/nginx/conf/conf.d/http
RUN mkdir -p /usr/local/nginx/conf/conf.d/stream
RUN mkdir -p /usr/local/nginx/conf/conf.d/key
RUN yum install -y cmake pcre pcre-devel openssl openssl-devel gd-devel \
    zlib-devel gcc gcc-c++ net-tools iproute telnet wget curl &&\
    yum clean all && \
    rm -rf /var/cache/yum/*
RUN wget http://nginx.org/download/nginx-1.19.6.tar.gz
RUN tar xf nginx-1.19.6.tar.gz
WORKDIR nginx-1.19.6
RUN ./configure --prefix=/usr/local/nginx --with-http_image_filter_module --user=www --group=www \
    --with-http_ssl_module --with-http_v2_module --with-http_stub_status_module \
    --with-stream --with-stream_ssl_preread_module --with-stream_ssl_module \
    --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log \
    --pid-path=/var/run/nginx/nginx.pid
RUN make -j 4 && make install && \
    rm -rf /usr/local/nginx/html/*  && \
    echo "hello word" >/usr/local/nginx/html/index.html  && \
    rm -rf nginx* && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN chown -R www.www /var/log/nginx
ENV LOG_DIR /var/log/nginx
ENV PATH $PATH:/usr/local/nginx/sbin
COPY ./conf.d/http/default.conf /usr/local/nginx/conf/conf.d/http/default.conf
COPY ./conf.d/stream/default.conf /usr/local/nginx/conf/conf.d/stream/default.conf
COPY ./conf.d/nginx.conf /usr/local/nginx/conf/nginx.conf
EXPOSE 80
EXPOSE 443
WORKDIR /usr/local/nginx
CMD ["nginx","-g","daemon off;"]
