# (base: https://github.com/dit4c/dockerfile-nghttpx)

FROM alpine:edge
LABEL maintainer="Ryo Ota <nwtgck@gmail.com>"

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    adduser -S -D -h /dev/null -s /sbin/nologin nghttpx && \
    apk --no-cache add nghttp2 tini

ENTRYPOINT ["tini", "--", "nghttpx", "--user=nghttpx"]
