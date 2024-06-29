# Enterprise Network re-design

## Challenges of Current Enterprise Network

Enterprise Network is expanding multiple data center and Clouds such as AWS, Azure, OCI and others. Data access is also expanding traditional WAN, SD-WAN, SASE and partner networks.
A typical Enterpise network uses L3 IP network to connect Data center, Clouds, ohter Data centers, Branch office and others. L3 network is managed by BGP, OSPF and static routes. Expanding L3 network makes complex routing configuration. Routing protocol between Data center and Clouds uses BGP, Routing protocol in Data center uses OSPF. SASE gateway uses BGP and VRRP. Routing injection and route aggrigation sometimes make routing black hole.
A network administrator needs to consider impact area carefully when the routing configuration modification. Because routing impact may affect entire enterprise network.  
Additionally, a network administrator shall consider private IPv4 address exhaustion and IP address conflict.

(add pic of enter network)

Typical data center network uses L2 Fabric or IP Fabric (EVPN-VXLAN). It connects Internet gateway, Branch office gateway (SD-WAN, SASE), IaaS (VM infra), physical servers and Sercurity devices. Networks are isolated by VLAN for respective applications.

(add pic of L2 netowrk in DC)

Application to application access manages typilically Firewall. Firewall connects multiple VLANs. ACL (Access list) is created across VALNs. If the IP address is dupulicated, SNAT/DNAT is also configured if required. Enterprise services keep glowing and large Firewall needs to operate more thouthans rules, in some case 10 thouthans or more. ACL configuration is complex, If shorter prefix rule overwrites longer prefix rule, traffic may be blocked unexpectedly or allowed unnececcary traffic.

(add pic of App App)

Data center and Cloud connectivity need roudting domain extention. Typical Cloud router doens't support VRFs. If network isolation is required between data center and clouds, respective overlay tunnel creation is one of solutions. Multiple overlay tunnel comsumes VM instance fee in clouds and managing configurations are messy work.
Even more, multiple clouds traffic would make its managemnt complex.

(add pic of hybric cloud)

Switching application from Datacenter to Datacenter of Clouds (or opporsite way) is complex operation. For instance, DNS A record modification from old one to new one. Because IP address of new application may be differnt from the existing application. Swiching application access by DNS modification takes some time for expiring DNS TTL and it also takes the same time for fallback.
L2 extension across data centers and clouds makes L2 BUM traffic and IP address dupilication issue. Switching application is done by configuration changing of network devices. Network devices connect multiple systems. If the opration is mitaken, failure area is huge.

(add pic of hybric cloud)

Network administrator/operator aim to Self service or network automation for Application access. But most of approach is automation of network configurations by Ansible. Self service requires Network service layer on Ansible. Designing and developpoing service layer need huge effort.

(add pic of Service layer)

## Network Abstraction layer in Enterprise Network

