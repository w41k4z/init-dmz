<!-- Setting the ip address of the interface eth0, eth1 and eth2 -->
ip addr add 192.168.10.1/24 dev eth0 <!-- LAN -->
ip addr add 10.0.0.1/24 dev eth1 <!-- DMZ -->
ip addr add 192.168.122.10/24 dev eth2 <!-- WAN -->

<!-- Default route pointing to WAN -->
ip route add default via 192.168.122.1

<!-- Use Google’s public DNS server -->
echo "nameserver 8.8.8.8" > /etc/resolv.conf

<!-- Enabling ip forwarding -->
echo 1 > /proc/sys/net/ipv4/ip_forward

<!-- DNAT config to expose public server to LAN through its eth0 interface (port: 8080) -->
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 8080 -j DNAT --to-destination 10.0.0.2:80

<!-- Enforce packet filtering -->
iptables -P FORWARD DROP

<!-- Allow HTTP 80 to public server -->
iptables -A FORWARD -p tcp -d 10.0.0.0/24 --dport 80 -j ACCEPT

<!-- Allow HTTPS 443 to public server -->
iptables -A FORWARD -p tcp -d 10.0.0.0/24 --dport 443 -j ACCEPT

<!-- Allow SSH 22 to public server -->
iptables -A FORWARD -p tcp -d 10.0.0.0/24 --dport 22 -j ACCEPT

<!-- Allow return traffic from public server to LAN -->
iptables -A FORWARD -p tcp -s 10.0.0.0/24 -m state --state ESTABLISHED,RELATED -j ACCEPT
