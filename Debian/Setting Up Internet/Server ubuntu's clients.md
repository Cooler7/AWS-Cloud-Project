Now to enable internet at the created clients, this includes: central.inova.pt, wazuh.inova.pt, www.inova.pt, these ones will use the graphical interface: sales.inova.pt, marketing.inova.pt

#To enter a client, first you need enter them via ssh like:

#first exit root

ssh -i key.pem ubuntu@HOSTNAME/IP  # its using the created key.pem and you can paste the IP which leads to the machine that you want to enter or hostname if you have DNS enabled

#For example:


ssh -i chave.pem ubuntu@172.31.100.101    #this one will enter the machine called: www.inova.pt the ubuntu part is the password

sudo hostnamectl set-hostname www.inova.pt  #sets the machine's hostname as www.inova.pt, exit then log in again to apply this effect

sudo su –   #enter root

cd /etc/netplan/   #navigate to this folder

cp 50-cloud-init.yaml 50-cloud-init.yaml_$(date -Is)   #I do this command to create a backup, because the next command if failed can be annoying to deal with

nano 50-cloud-init.yaml   #edit the file, DO NOT USE TAB BUTTON

#edit the file like this:

![image](https://user-images.githubusercontent.com/32963070/154146751-a49ab10a-5d93-4994-97ab-644716184de4.png)


#after enabling DNS you can change the  [ 8.8.8.8 ] to the ip from your server that comes from the cloud

netplan try   #this will attempt to enable the previous change, if it's incorrect you can revert it, if it's accept just press ENTER and then ping to the internet

ping 1.1.1.1

#if packets are sent CONGRATS! You just enabled the internet on a client which is connected to a main server
#now do the same steps as above to the other clients
