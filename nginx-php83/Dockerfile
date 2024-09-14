FROM alpine:3.20.3
ENV UPLOAD_MAX_SIZE=10G \
    APC_SHM_SIZE=128M \
    OPCACHE_MEM_SIZE=128 \
    MEMORY_LIMIT=512M \
    CRON_PERIOD=15m \
    CRON_MEMORY_LIMIT=1g \
    TZ=Asia/Shanghai \
    DOMAIN=localhost

# add nginx + php83
RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
     && apk update \
     && apk add --no-cache tzdata  \
         php83-bcmath \
         php83-common \
         php83-curl \
         php83-dom \
         php83-fileinfo \
         php83-fpm \
         php83-iconv \
         php83-mbstring \
         php83-mysqli \
         php83-mysqlnd \
         php83-openssl \
         php83-opcache \
         php83-pcntl \
         php83-pdo \
         php83-pdo_mysql \
         php83-pdo_sqlite \
         php83-phar \
         php83-posix \
         php83-session \
         php83-simplexml \
         php83-sockets \
         php83-sqlite3 \
         php83-tokenizer \
         php83-xml \
         php83-xmlwriter \
         php83-zip \
         s6 \
         nginx \
         tzdata \
         curl \
         libevent \
      && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
      && echo "Asia/Shanghai" > /etc/timezone \
# 拷贝nginx和php配置文件 和替换环境变量
COPY /config/php/php.ini /etc/php83/php.ini
COPY /config/php/fpm-pool.conf /etc/php83/php-fpm.conf
COPY /config/nginx/conf/nginx.conf /etc/nginx/nginx.conf
RUN sed -i -e "s/<UPLOAD_MAX_SIZE>/$UPLOAD_MAX_SIZE/g" /etc/nginx/nginx.conf

## 配置定时器
COPY /supercronic /usr/local/bin/
RUN mkdir /webser \
    && >/webser/supercronic_cron
# 修改目录权限
RUN mkdir -p /var/log/php83 \
    && mkdir -p /var/log/nginx\
    && chown -R nobody.nobody /var/log/php83 \
    && chown -R nobody.nobody /var/log/nginx \
    && chown -R nobody.nobody /run
# s6配置
COPY --chown=nobody.nobody /config/s6.d /etc/s6
ENTRYPOINT ["/bin/s6-svscan" ,"/etc/s6"]