First you have to navigate to control.enta.pt, setup the basic configurations like internet and dns and then when you are ready to enable certificates do this:

cd /etc/easy-rsa/

nano vars

Edit this

set_var EASYRSA_DN     "org"

set_var EASYRSA_REQ_COUNTRY    "PT"

set_var EASYRSA_REQ_PROVINCE   "Azores"

set_var EASYRSA_REQ_CITY       "São Miguel"

set_var EASYRSA_REQ_ORG        "ENTA"

set_var EASYRSA_REQ_EMAIL      "mail@enta.pt"

set_var EASYRSA_REQ_OU         "GRSI 1"

./easyrsa init-pki    #initiates the key

./easyrsa build-ca   #creates certificate called ca.crt

#use password called: Passw0rd



cd /etc/easy-rsa/

nano vars

#Edit the file and setup your organization details

set_var EASYRSA_DN     "org"

set_var EASYRSA_REQ_COUNTRY    "PT"

set_var EASYRSA_REQ_PROVINCE   "Azores"

set_var EASYRSA_REQ_CITY       "São Miguel"

set_var EASYRSA_REQ_ORG        "INOVA"

set_var EASYRSA_REQ_EMAIL      "webmaster@inova.pt"

set_var EASYRSA_REQ_OU         "GRSI"

./easyrsa init-pki

./easyrsa build-ca subca   #this sub-ca is important because it uses the control.inova.pt as a subordinate certificate server of control.enta.pt and after this we can use it to create as many certificates as we need

clear # clears your console because we need some space for the next command

cat /etc/easy-rsa/pki/reqs/ca.req  # copy all of this because its the requirement to use certificates

#at control.enta.pt paste the one you copied here:

nano /etc/easy-rsa/pki/reqs/inova_ca.crt  #creates the file then paste it

./easyrsa sign-req ca inova_ca   #sign it

cat /etc/easy-rsa/pki/ca.crt >> /etc/easy-rsa/pki/issued/inova_ca.crt  #prints the contents

cp /etc/easy-rsa/pki/ca.crt /etc/pki/tls/certs/inova_ca.crt  #paste it

clear 

cat /etc/easy-rsa/pki/issued/ca_inova.crt  #prints the content 


#At control.inova.pt, paste it here:

nano /etc/easy-rsa/pki/ca.crt






