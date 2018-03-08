FROM alpine:3.6
LABEL maintainer="roy<zhushaoqing@ispied.com>"

# 换为国内镜像，以加速docker image制作速度，非中国镜内用户请注释掉下一行
RUN echo 'http://mirrors.aliyun.com/alpine/v3.6/main' > /etc/apk/repositories \
    && echo '@community http://mirrors.aliyun.com/alpine/v3.6/community' >> /etc/apk/repositories \
    && echo '@testing http://mirrors.aliyun.com/alpine/edge/testing' >> /etc/apk/repositories \
    && echo '@edge https://mirrors.aliyun.com/alpine/edge/main' >> /etc/apk/repositories 
RUN apk update && apk upgrade
RUN apk add --upgrade apk-tools@edge
#时区配置
ENV TIMEZONE Asia/Shanghai
RUN apk add tzdata && ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo $TIMEZONE > /etc/timezone