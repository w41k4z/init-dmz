<!-- Setting ip address of the interface -->
ip addr add 192.168.10.2/24 dev eth0

<!-- Setting default route -->
ip route add default via 192.168.10.1 dev eth0

<!-- Use Google’s public DNS server -->
echo "nameserver 8.8.8.8" > /etc/resolv.conf
