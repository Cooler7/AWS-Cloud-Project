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

