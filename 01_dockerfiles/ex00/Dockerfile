FROM alpine:latest

MAINTAINER Mehdi El kaddouri <mehel-ka@student.42.fr>

RUN apk update && \
    apk add vim && \
    rm -rf /var/cache/apk/*

CMD ["/usr/bin/vim"]
