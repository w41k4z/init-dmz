FROM alpine:latest

LABEL description="DMZ Firewall"

RUN apk update && apk add --no-cache \
    iptables \
    iproute2 \
    tcpdump \
    iputils \
    net-tools \
    curl \
    bash

CMD ["/bin/sh"]
