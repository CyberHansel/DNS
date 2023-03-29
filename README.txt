# DNS

$ nslookup 140.1.1.200.in-addr.arpa              #Looks for PTR record for ip address 200.1.1.140 !!! (IP in PTR is Reverse)
$ nslookup -type=PTR 140.1.1.200.in-addr.arpa    #I think it's same command as previous.

$ nslookup -type=SOA example.com                 #To determine whether a DNS server is authoritative for a particular zone.

"Non-authoritative answer" indicates that the DNS server that provided the response is not the authoritative source for the domain you queried. DNS server that you
                           contacted does not directly manage the DNS records for "example.com", but it has retrieved the information from another DNS server that is
                           authoritative for that domain.



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
sudo netplan --debug apply #to see what happening when applying changes  


update add mail.example.com. IN A 192.168.1.3  
update add 192.168.1.3.in-addr.arpa. IN PTR mail.example.com.   
 

`nslookup example.com`  display the IP address of the name server that was used to resolve the domain name "example.com".    

