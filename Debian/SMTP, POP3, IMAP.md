#At central.inova.pt we will create an email server to send email. Each created user will have a different protocol attached to the user.

#At a client with GUI like sales.inova.pt:

adduser maria  #creates user called maria

adduser miguel  #creates user called miguel

adduser jorge  #creates user called jorge

cp /home/ubuntu/.xsession /home/maria/.xsession   

chown maria:maria /home/maria/.xsession   #gives permissions to maria's session to use RDP after

cp /home/ubuntu/.xsession /home/miguel/.xsession

chown miguel:miguel /home/miguel/.xsession

cp /home/ubuntu/.xsession /home/jorge/.xsession

chown jorge:jorge /home/jorge/.xsession



#after go to the email server in this case central.inova.pt:

sudo su -
 apt -y install postfix postfix-doc dovecot-imapd dovecot-pop3d sasl2-bin

- enta.pt
 dpkg-reconfigure postfix

- enta.pt

- ubuntu

- Skip

- No

- Clear the line

- 0

- +

- ipv4

nano /etc/postfix/main.cf

#Change

smtpd_tls_cert_file=/etc/ssl/certs/azores.pt.crt

smtpd_tls_key_file=/etc/ssl/private/azores.pt.key

nano /etc/postfix/master.cf

#uncomment 1º Group:

submission inet n       -       y       -       -       smtpd

-o syslog_name=postfix/submission

-o smtpd_tls_security_level=encrypt

-o smtpd_sasl_auth_enable=yes

#Add bellow -o smtpd_sasl_auth_enable=yes:

-o smtpd_client_restrictions=permit_sasl_authenticated,reject
   

#uncomment 2º Group:

smtps     inet  n       -       y       -       -       smtpd

-o syslog_name=postfix/smtps

-o smtpd_tls_wrappermode=yes

-o smtpd_sasl_auth_enable=yes

-o smtpd_client_restrictions=permit_sasl_authenticated,reject


nano /etc/postfix/sasl/smtpd.conf

#Add

pwcheck_method: saslauthd

mech_list: PLAIN LOGIN
 
 nano /etc/default/saslauthd

#EDIT

START=yes

OPTIONS="-c -m /var/spool/postfix/var/run/saslauthd"

 postconf -e 'home_mailbox = Maildir/'

nano /etc/dovecot/conf.d/10-auth.conf

#Uncomment and EDIT

disable_plaintext_auth = no

nano /etc/dovecot/conf.d/10-mail.conf

#UNCOMMENT

mail_location = maildir:~/Maildir

#comment

#mail_location = mbox:~/mail:INBOX=/var/mail/%u

nano /etc/dovecot/conf.d/10-ssl.conf

 > ssl = yes

#UNCOMMENT AND EDIT:

ssl_cert = </etc/ssl/certs/azores.pt.crt

ssl_key = </etc/ssl/private/azores.pt.key

cd /etc/skel/

 > maildirmake.dovecot Maildir
 adduser postfix sasl

adduser dovecot sasl

systemctl restart saslauthd.service postfix dovecot

sudo su -

cd /etc/skel

> maildirmake.dovecot Maildir

adduser maria

adduser miguel

adduser jorge

#check ports 
ss -tulp | grep master

 ss -tulp | grep dovecot
 
 #Copy the certificates created at control.inova.pt and paste them here:
   
   > "/etc/ssl/certs/azores.pt.crt"
   
   > "/etc/ssl/private/azores.pt.key"


#To finish go to sales.inova.pt

 # Exit root.
 
 sudo apt install -y xfce4 xfce4-goodies
 
 - lightdm
 
 sudo apt install -y xrdp chromium-browser filezilla thunderbird   #chromium is the web browser that we are going to use, filezilla is the FTP program and thunderbird is the email server
 
 sudo adduser xrdp ssl-cert
 
 echo xfce4-session > ~/.xsession
 
 sudo reboot
 
 
 #after all of that, use RDP like windows remote desktop or REMNINA at Linux systems to use the remote desktop client to send and recieve email
 #setup an account, and use the protocols you established
