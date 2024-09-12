# Use your favorite image
FROM alpine
ENV TZ=Asia/Shanghai

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
      && mkdir -p /etc/s6
ENTRYPOINT ["/bin/s6-svscan" ,"/etc/s6"]