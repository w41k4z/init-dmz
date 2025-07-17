FROM alpine:latest

LABEL description="LAN internal desktop"

RUN apk update && apk add --no-cache \
    iproute2 \
    iputils \
    curl \
    bash \
    net-tools \
    tcpdump

CMD ["/bin/sh"]
