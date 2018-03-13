FROM vitamin/alpine:3.6
LABEL maintainer="roy<zhushaoqing@ispied.com>"


ENV VITAMIN_USER="vitaminbox" \
	VITAMIN_GROUP="vitaminbox" \
	VITAMIN_UID="1000" \
        VITAMIN_GID="1000"

ENV MYSQL_BASE_INCL="/etc/my.cnf.d" \
    MYSQL_CUST_INCL1="/etc/mysql/conf.d" \ 
    MYSQL_CUST_INCL2="/etc/mysql/docker-default.d" \
    MYSQL_DEF_DAT="/var/lib/mysql" \
    MYSQL_DEF_LOG="/var/log/mysql" \
    MYSQL_DEF_PID="/var/run/mysqld" \
    MYSQL_DEF_SCK="/var/sock/mysqld" \
    MYSQL_LOG_SLOW="${MYSQL_DEF_LOG}/slow.log" \ 
    MYSQL_LOG_ERROR="${MYSQL_DEF_LOG}/error.log" \
    MYSQL_LOG_QUERY="${MYSQL_DEF_LOG}/query.log"

RUN apk --update add mysql mysql-client pwgen && rm -f /var/cache/apk/* && \
echo "Success"
COPY ./scripts/run.sh /scripts/run.sh
RUN mkdir /scripts/pre-exec.d && \
mkdir /scripts/pre-init.d && \
chmod -R 755 /scripts

VOLUME [ "${MYSQL_DEF_LOG}", "${MYSQL_DEF_DAT}"]
EXPOSE 3306
VOLUME ["/var/lib/mysql"]

ENTRYPOINT ["/scripts/run.sh"]