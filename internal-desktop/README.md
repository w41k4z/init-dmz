<!-- Setting ip address of the interface -->
ip addr add 192.168.10.2/24 dev eth0

<!-- Setting default route -->
ip route add default via 192.168.10.1 dev eth0
