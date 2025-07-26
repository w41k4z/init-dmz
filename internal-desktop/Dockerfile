FROM alpine:latest

LABEL description="LAN internal desktop"

RUN apk update && apk add --no-cache \
    iproute2 \
    iputils \
    curl \
    bash \
    net-tools \
    tcpdump


# Set proxy environment variables globally inside the container
ENV http_proxy="http://192.168.10.1:3128"
ENV https_proxy="http://192.168.10.1:3128"

CMD ["/bin/sh"]
