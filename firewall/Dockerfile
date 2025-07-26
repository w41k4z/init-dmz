FROM alpine:latest

LABEL description="DMZ Firewall"

RUN apk update && apk add --no-cache \
    iptables \
    iproute2 \
    tcpdump \
    iputils \
    net-tools \
    curl \
    squid \
    bash

# Create necessary directories
RUN mkdir -p /etc/squid /var/log/squid /var/cache/squid

# Copy config and blacklist into image
COPY squid.conf /etc/squid/squid.conf
COPY blacklist.txt /etc/squid/blacklist.txt

CMD ["/bin/sh"]
