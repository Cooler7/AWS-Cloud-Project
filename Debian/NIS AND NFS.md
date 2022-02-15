#We need central.inova.pt as server and clients we will use sales.inova.pt and marketing.inova.pt
#so 1 server and 2 clients

 nano /etc/hosts

#Add this right here: "ipserver" central.inova.pt central inova.pt (Change the IP)

apt update && apt -y upgrade && apt install nfs-kernel-server

nano /etc/exports

Add: /var/homes *(rw,sync,no_subtree_check,no_root_squash)

mkdir /var/homes

exportfs -a

systemctl enable --now nfs-kernel-server

adduser manuel --home /var/homes/manuel

echo xfce4-session > /var/homes/manuel/.xsession

chown manuel:manuel /var/homes/manuel/.xsession

#go to sales.inova.pt to setup NFS

 apt update && apt -y upgrade && apt install nfs-common

nano /etc/hosts

A#dd this line: "ipserver"  central.inova.pt central inova.pt  (Change IP and its the same as above)

mkdir /var/homes

mount -t nfs 172.31.20.30:/var/homes /var/homes/  (Change IP)

cat /etc/mtab

#Copy the line above paste here ( /etc/fstab ) and add ,nofail

#then reboot your machine and hope it does not cause an error!

-------------------------------------------------------------------------------------------------------------------------------------------

NIS SETUP

#at central.inova.pt

apt -y install nis

- NIS DOMAIN: enta.pt

nano /etc/default/nis

- NISSERVER=master

nano /etc/ypserv.securenets

# This line gives access to everybody. PLEASE ADJUST! (change 0.0.0.0 / 0.0.0.0 to mask and private network)

255.255.255.0         "private ipserver"

# add to the end: IP range you allow to access

255.255.255.0         "private ipserver"

nano /var/yp/Makefile

- MERGE_PASSWD=true

- MERGE_GROUP=true

Update Database: /usr/lib/yp/ypinit -m

list, type a <control D>.

 next host to add:  entasrv.enta.pt
 
 next host to add:       #simply use CTRL + D
 
 The current list of NIS servers looks like this:

 systemctl restart nis

# after nis restart If you added users in local server, apply them to NIS database like so:
 
 - cd /var/yp
 
 - make

-----------------------------------------------------------------------------------------------------
 
 #at sales.inova.pt
 
  
apt -y install nis

 - NIS DOMAIN: inova.pt

nano /etc/yp.conf

 # ypserver ypserver.network.com
 
 # add to the end: [domain name] [server] [NIS server's hostname]
 
 domain enta.pt server entasrv.enta.pt

 nano /etc/nsswitch.conf
 
 - passwd: #add "nis" to the end
 
 - group: #add "nis" to the end
 
 - shadow: #add "nis" to the end
 
 - hosts: #add "nis" to the end

 nano /etc/pam.d/common-session
 
 - #add: session optional        pam_mkhomedir.so skel=/etc/skel umask=077

 systemctl restart nis

 #when root use: login   
 
 - User that you have created early.  #in this case manuel
 
 - Password.


 
 
 #install GUI 
 
  Leave root.

 sudo apt install -y xfce4 xfce4-goodies
 
 - lightdm

 sudo apt install -y xrdp chromium-browser 

 sudo adduser xrdp ssl-cert

 echo xfce4-session > ~/.xsession

 sudo reboot
