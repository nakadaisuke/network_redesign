# Enterprise Network re-design

## Challenges of Current Enterprise Network

Enterprise Network is expanding multiple data center and Clouds such as AWS, Azure, OCI and others. Data access is also expanding traditional WAN, SD-WAN, SASE and partner networks.
A typical Enterpise network uses L3 IP network to connect Data center, Clouds, ohter Data centers, Branch office and others. L3 network is managed by BGP, OSPF and static routes. Expanding L3 network makes complex routing configuration. Routing protocol between Data center and Clouds uses BGP, Routing protocol in Data center uses OSPF. SASE gateway uses BGP and VRRP. Routing injection and route aggrigation sometimes make routing black hole.
A network administrator needs to consider impact area carefully when the routing configuration modification. Because routing impact may affect entire enterprise network.  
Additionally, a network administrator shall consider private IPv4 address exhaustion and IP address conflict.

(add pic of enter network)

Typical data center network uses L2 Fabric or IP Fabric (EVPN-VXLAN). It connects Internet gateway, Branch office gateway (SD-WAN, SASE), IaaS (VM infra), physical servers and Sercurity devices. Networks are isolated by VLANs of Fabric or virtual netowrk in IaaS for respective applications.

(add pic of L2 netowrk in DC)

Application to application access manages typilically Firewall. Firewall connects multiple VLANs. ACL (Access list) is created across VALNs. If the IP address is dupulicated, SNAT/DNAT is also configured if required. Enterprise services keep glowing and large Firewall needs to operate more thouthans rules, in some case 10 thouthans or more. ACL configuration is complex, If shorter prefix rule overwrites longer prefix rule, traffic may be blocked unexpectedly or allowed unnececcary traffic.

(add pic of App App)

Data center and Cloud connectivity need roudting domain extention. Typical Cloud router doens't support VRFs. If network isolation is required between data center and clouds, respective overlay tunnel creation is one of solutions. Multiple overlay tunnel comsumes VM instance fee in clouds and managing configurations are messy work.
Even more, multiple clouds traffic would make its managemnt complex.

(add pic of hybric cloud)

Switching application from Datacenter to Datacenter of Clouds (or opporsite way) is complex operation. For instance, DNS A record modification from old one to new one. Because IP address of new application may be differnt from the existing application. Swiching application access by DNS modification takes some time for expiring DNS TTL and it also takes the same time for fallback.
L2 extension across data centers and clouds makes L2 BUM traffic and IP address dupilication issue. Switching application is done by configuration changing of network devices. Network devices connect multiple systems. If the opration is mitaken, failure area is huge.

(add pic of hybric cloud)

Kubernetes (and regarding distributions like OpenShift, EKS) connectivity is challenge because Kubernetes abstructs network inside. Only node IP address is exposed to external network. Typical Firewall cannot identify source applications by IP address, because source IP address is SNATed by Kubernetes node. Typical enterprise network devides different networks by VLANs. For instance, User access network, Application network, Database network are isolated. When applicaion on Kubernetes needs to access these three networks, but it is hard to connects multiple VLANs. If L3 level isolation is required, BGP session shall be separated.

(add pic of Kubernetes)

Network administrator/operator aim to Self service or network automation for Application access. But most of approach is automation of network configurations by Ansible. Self service requires Network service layer on Ansible. Designing and developpoing service layer need huge effort.

(add pic of Service layer)

## Application access challenges

Application acccess is complex. One application accesses different application and application recives traffic from multiple clients, Branch office, Laptop, mobile or others.
(describe Source/Destination L3/L4 access control is limit of operation)

## Data center and clouds access challenges

L3VPN between DC and Clouds. Distributed LB between DC and Clouds.

## IP address conflict challenges

Current solution is complex SANT/DNAT + ACL operation.

## Re-desiging Enterprise network
Describe how Network abstraction layer works and its required functions. Modules Network service

## The road of Self operation Network



