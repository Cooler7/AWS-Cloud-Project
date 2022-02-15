#at www.enta.pt


#generate a certificate like : www.enta.pt.crt and add the key

nano /etc/nginx/nginx.conf   #edit this file

#and then edit like this:
server {

listen 443 ssl;

server_name www.enta.pt;

ssl_certificate /etc/nginx/cert/certificate.crt;

ssl_certificate_key /etc/nginx/cert/private.key;

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

ssl_ciphers HIGH:!aNULL:!MD5;
}


