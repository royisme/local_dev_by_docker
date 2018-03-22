FROM vitamin/alpine:3.6
LABEL maintainer="roy<zhushaoqing@ispied.com>"
ENV REDIS_VERSION=4.0.0
RUN apk update && apk upgrade
RUN set -exo pipefail \
  && apk add --no-cache --virtual .build-deps \
    build-base \
    linux-headers \
    openssl \
  && wget -O /usr/local/bin/gosu https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64 \
  && chmod +x /usr/local/bin/gosu \
  && cd /tmp \
  && wget https://github.com/antirez/redis/archive/${REDIS_VERSION}.tar.gz \
  && tar xzf ${REDIS_VERSION}.tar.gz \
  && cd /tmp/redis-${REDIS_VERSION} \
  && make \
  && make install \
  && cp redis.conf /etc/redis.conf \
  && sed -i -e 's/bind 127.0.0.1/bind 0.0.0.0/' /etc/redis.conf \
  && adduser -D redis \
  && apk del .build-deps \
  && rm -rf /tmp/* \
  && addgroup -g 82 -S www-data \
  && adduser -u 82 -D -S -G www-data www-data
EXPOSE 6379
VOLUME ["/data"]
CMD ["redis-server", "/etc/redis.conf"]
