FROM alpine:latest

MAINTAINER Aslan MALSAGOV <amalsago@student.42.fr>

RUN apk update && \
    apk add vim && \
    rm -rf /var/cache/apk/*

CMD ["/usr/bin/vim"]
