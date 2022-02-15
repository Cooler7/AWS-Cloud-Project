
#at control.enta.pt

yum update

 yum install iptables-services

 systemctl enable --now iptables

 iptables -F

 iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

 iptables -t nat -L -nv

 service iptables save

 nano /etc/sysctl.conf

 net.ipv4.ip_forward=1

 sysctl -p 

service network restart


#Setting up internet at a client

 sudo su –

nano /etc/sysconfig/network-scripts/ifcfg-eth0

GATEWAY="server ip"

systemctl status network

systemctl restart network

ping 1.1.1.1

yum update
