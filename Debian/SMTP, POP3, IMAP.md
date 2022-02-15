#At central.inova.pt we will create an email server to send email. Each created user will have a different protocol attached to the user.

#At a client with GUI like sales.inova.pt:

adduser maria
adduser miguel
 adduser jorge
 cp /home/ubuntu/.xsession /home/maria/.xsession
 chown maria:maria /home/maria/.xsession
 cp /home/ubuntu/.xsession /home/miguel/.xsession
 chown miguel:miguel /home/miguel/.xsession
 cp /home/ubuntu/.xsession /home/jorge/.xsession
 chown jorge:jorge /home/jorge/.xsession
