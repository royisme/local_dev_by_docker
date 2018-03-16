FROM vitamin/alpine:3.6
LABEL maintainer="roy<zhushaoqing@ispied.com>"


ENV VITAMIN_USER="vitaminbox" \
	VITAMIN_GROUP="vitaminbox" \
	VITAMIN_UID="1000" \
    VITAMIN_GID="1000"

RUN apk --update add bind  && addgroup -g ${VITAMIN_GID} -S ${VITAMIN_GROUP} \
    && adduser -u ${VITAMIN_UID} -D -S -G ${VITAMIN_USER} ${VITAMIN_GROUP}
COPY ./scripts/init.sh /
EXPOSE 53
EXPOSE 53/udp
RUN ["chmod", "+x","/init.sh" ]
ENTRYPOINT ["/init.sh"]
