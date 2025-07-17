FROM alpine:latest

LABEL description="Public web server"

RUN apk update && apk add --no-cache \
    lighttpd \
    bash \
    curl \
    iproute2 \
    iputils \
    net-tools

RUN echo "<h1>Hello from DMZ Web Server</h1>" > /var/www/localhost/htdocs/index.html

CMD ["/usr/sbin/lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
