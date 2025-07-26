<!-- Setting ip address of the interface -->
ip addr add 10.0.0.2/24 dev eth0

<!-- Setting default route to resolve return traffic from different network -->
ip route add default via 10.0.0.1 dev eth0
