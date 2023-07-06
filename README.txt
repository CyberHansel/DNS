$ ip route show        #shows the routing entries that define how network packets are forwarded or routed within the system
$ ip -br a show        #brief or concise view of the system's network interfaces and their configurations, -br option stands for "brief


# DNS
## NSLOOKUP

$ nslookup example.com                           #requests data about DNS server.
$ nslookup 140.1.1.200.in-addr.arpa              #Looks for PTR record for ip address 200.1.1.140 !!! (IP in PTR is Reverse)
$ nslookup -type=PTR 140.1.1.200.in-addr.arpa    #I think it's same command as previous.

$ nslookup -type=SOA example.com                 #To determine whether a DNS server is authoritative for a particular zone. If the DNS server is authoritative for the
                                                  zone, it should return the Start of Authority (SOA) record for the domain.

"Non-authoritative answer" indicates that the DNS server that provided the response is not the authoritative source for the domain you queried. DNS server that you
                           contacted does not directly manage the DNS records for "example.com", but it has retrieved the information from another DNS server that is
                           authoritative for that domain.
## DIG
$ dig google.com @ns.test.com              #querying the DNS records for "google.com" from specific the DNS server ns.test.com

$ dig +noall +answer @<nameserver_ip> www.example.com               #Request  for A record
$ dig +noall +answer @<nameserver_ip> -x 192.168.1.1                #reverse DNS lookups for PTR record of example.com
$ nslookup -query=ptr 1.1.168.192.in-addr.arpa <nameserver_ip>      #Alternative to query PTR record about 192.168.1.1 from DNS server
The "+noall +answer" options are used to make the output of the command more concise and display only the answer section of the response.


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

