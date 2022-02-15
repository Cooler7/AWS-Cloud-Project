#installing vsftpd on ubuntu at www.inova.pt

apt install vsftpd

systemctl status vsftpd

#after creating the ftp.inova.pt at control.inova.pt (which uses the same steps as the www but its ftp)

#copy the ftp ca to: /etc/ssl/certs and the key to: /etc/ssl/certs/private then add the permissions as below:

chmod --reference=ssl-cert-snakeoil.key ftp.inova.pt.key

chown --reference=ssl-cert-snakeoil.key ftp.inova.pt.key

nano /etc/vsftpd.conf

#uncoment 

write_enable=YES
    
#I used explicit FTP for this project copy and paste this at the end of the file:

change ssl_enable=NO -> YES
 #then add:
 
pasv_enable=YES

pasv_min_port=PORT1   #port 1 

pasv_max_port=PORT2   #port 2

allow_anon_ssl=NO

force_local_data_ssl=YES

force_local_logins_ssl=YES

ssl_tlsv1=YES

ssl_sslv2=NO

ssl_sslv3=NO

require_ssl_reuse=NO

ssl_ciphers=HIGH

systemctl restart vsftpd  #restarts the service and checks for errors


