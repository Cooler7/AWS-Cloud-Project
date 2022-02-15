#now to enable http and https on www.inova.pt

#at control.inova.pt:
iptables -t nat -A PREROUTING -i eth0 -p tcp -m tcp --dport 3389 -j DNAT --to-destination "ip of www server"   # enable iptables ports that use http and https

iptables -t nat -A PREROUTING -i eth0 -p tcp -m tcp --dport 80 -j DNAT --to-destination "ip of www server"  

netfiler-persistent reload
netfiler-persistent save 

#now to enable a certificate for www.inova.pt

sudo su -
> apt install easy-rsa
> cp -r /usr/share/easy-rsa/ /etc/
> cd /etc/easy-rsa/
> nano openssl-easyrsa.conf
> comentar RANDFILE
> mv vars.example vars
./easyrsa build-server-full www.inova.pt nopass  
