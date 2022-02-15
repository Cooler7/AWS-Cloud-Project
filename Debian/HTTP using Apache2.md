#now to enable http and https on www.inova.pt

#at control.inova.pt:
iptables -t nat -A PREROUTING -i eth0 -p tcp -m tcp --dport 3389 -j DNAT --to-destination "ip of www server"   # enable iptables ports that use http and https

iptables -t nat -A PREROUTING -i eth0 -p tcp -m tcp --dport 80 -j DNAT --to-destination "ip of www server"  

netfiler-persistent reload
netfiler-persistent save 

#now to enable a certificate for www.inova.pt

sudo su -

apt install easy-rsa

cp -r /usr/share/easy-rsa/ /etc/

cd /etc/easy-rsa/  #whenever you want to build a certificate always navigate to this page first then build using ./easyrsa

nano openssl-easyrsa.conf

#coment #RANDFILE

mv vars.example vars

./easyrsa build-server-full www.inova.pt nopass  # nopass to avoid extra passwords  the www part it's only to differentiate from other certificates

#at www.inova.pt

#copy your newly created certificate and paste it here:

cd /etc/ssl/certs/

#and paste the generated key here probably called www.inova.pt.key:

cd /etc/ssl/cers/private

chmod --reference=ssl-cert-snakeoil.key www.inova.pt.key
chown --reference=ssl-cert-snakeoil.key www.inova.pt.key   #gives permissions to the files



#Now we we actually install Apache2 after the certificates are set

apt install apache2

a2enmod ssl

a2ensite default-ssl.conf

systemctl restart apache2

nano /etc/apache2/sites-available/default-ssl.conf

change DocumentRoot > htmls

#change the names of the certificates with the ones you used

cd /var/www/

cp -r html/ htmls

cd html/

> index.html  #copy to index.html

nano index.html  #changing the http version  put a random word like HTTP UNSAFE

cd htmls/

> index.html

nano index.html #change to the HTTPS version write: HTTPS  WEB PAGE SECURED

systemctl restart apache2  #restart the service
