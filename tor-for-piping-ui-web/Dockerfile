FROM alpine:3.14.2

LABEL maintainer="Ryo Ota <nwtgck@gmail.com>"

# Install Tor
RUN apk --no-cache add tor

ENTRYPOINT [ "sh" ]
# NOTE: The order of chown and su is important
CMD [ "-c", \
      "chmod -R go-rwx /var/lib/tor/ && \
      chown -R tor /var/lib/tor/ && \
      su -s /bin/sh tor -c tor" \
    ]
