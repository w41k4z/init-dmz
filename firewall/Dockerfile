FROM ubuntu:latest

LABEL description="DMZ Firewall with Squid and Snort"

RUN apt-get update && apt-get install -y \
    iptables \
    iproute2 \
    tcpdump \
    iputils-ping \
    net-tools \
    curl \
    squid \
    snort \
    bash \
    && rm -rf /var/lib/apt/lists/*

# Create necessary directories
RUN mkdir -p /etc/squid /var/log/squid /var/cache/squid
RUN mkdir -p /etc/snort /var/log/snort


# Copy configs and blacklist into image
COPY squid.conf /etc/squid/squid.conf
COPY snort.conf /etc/snort/snort.conf
COPY blacklist.txt /etc/squid/blacklist.txt

CMD ["/bin/bash"]
