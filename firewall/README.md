<!-- Setting the ip address of the interface eth0, eth1 and eth2 -->
ip addr add 192.168.10.1/24 dev eth0 <!-- LAN -->
ip addr add 10.0.0.1/24 dev eth1 <!-- DMZ -->
ip addr add 192.168.122.10/24 dev eth2 <!-- WAN -->

<!-- Default route pointing to WAN -->
ip route add default via 192.168.122.1

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

<!-- Allow return traffic from public server using tcp -->
iptables -A FORWARD -p tcp -s 10.0.0.0/24 -m state --state ESTABLISHED,RELATED -j ACCEPT


<!-- NAT configuration to connect WAN to LAN -->
iptables -t nat -A POSTROUTING -o eth2 -s 192.168.10.0/24 -j SNAT --to-source 192.168.122.10

<!-- Allow LAN to WAN -->
iptables -A FORWARD -i eth0 -o eth2 -s 192.168.10.0/24 -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT

<!-- Allow WAN to return traffic only from established and related connection -->
iptables -A FORWARD -i eth2 -o eth0 -d 192.168.10.0/24 -m state --state ESTABLISHED,RELATED -j ACCEPT
