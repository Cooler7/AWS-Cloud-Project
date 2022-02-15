After your machines are created and set up, we can start enabling them to connect to the internet so we can install packages and other usefull tools.

At control.inova.pt which is the main server at the Debian side lets first on EC2 at AWS select Networking, change source/destination check and then tick STOP like this:
![image](https://user-images.githubusercontent.com/32963070/154142996-1be2f0b1-912c-4c53-b7fa-c866a87f9d0d.png)

This will allow connectivity between the machine and the cloud.

then follow these steps:

sudo hostnamectl set-hostname control.inova.pt    #setting up a hostname for your machine

nano key.pem    #create a key, in this case I called mine chave.pem

#after you have to copy the content of your kechmod 400y (the key that you used to create your machine and then paste here!)

chmod 600 key.pem  #this is used to give permissions to the key to be used for other hosts

apt-get update && apt upgrade -y   #this updates your machine

apt install netfilter-persistent iptables-persistent  #installing iptables

#if you need to manually edit your iptables you can use this command:

nano /etc/iptables/rules.v4

#after updating your iptables first reload them then save them in you ram like this:
#it also organizes your iptables 
netfilter-persistent reload

netfilter-persistent save

#next

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE  #allow postrouting

iptables -t nat -L -nv

netfilter-persistent save


#now to enable ipv4 forwarding:

nano /etc/sysctl.conf

#uncomment, just remove the hashtag
#before

#net.ipv4.ip_forward=1

#after
net.ipv4.ip_forward=1

#then hit CTRL + X then Y then ENTER to save your configuration for that file

sysctl -p #to confirm that it is enabled

Now we have to enable the internet to the other machines linked to this one via IP'S
