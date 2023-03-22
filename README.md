# DNS
/etc/netplan  
cat /etc/resolv.conf    nameserver 1.1.1.1    

22.04 >  
sudo mkdir /etc/systemd/resolved.conf.d/  
sudo nano /etc/systemd/resolved.conf.d/dns_servers.conf  
Add to created conf file:  
`[Resolve]`  
`DNS=8.8.8.8 1.1.1.1`  
sudo systemctl restart systemd-resolved


vai  
cd /etc/netplan 
sudo nano 01-network-manager.yaml  

  
  
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens160:
      dhcp4: no
      addresses:
        - 192.168.17.100/24
      gateway4: 192.168.17.2
      nameservers:
          addresses: [1.1.1.1, 8.8.8.8, 4.4.4.4]

sudo netplan try  
sudo netplan apply


update add mail.example.com. IN A 192.168.1.3  
update add 192.168.1.3.in-addr.arpa. IN PTR mail.example.com.   
 

`nslookup example.com`  display the IP address of the name server that was used to resolve the domain name "example.com".    

