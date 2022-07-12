- [Az Config Network And Endpoints](#az-config-network-and-endpoints)
  - [System routes](#system-routes)
  - [User defined routes](#user-defined-routes)
    - [attribs](#attribs)
    - [assoc](#assoc)
  - [Endpoint uses](#endpoint-uses)
    - [Why](#why)
    - [Add svc endpoint](#add-svc-endpoint)
  - [Private Link uses](#private-link-uses)
# Az Config Network And Endpoints 

## System routes
* direct traffic between VMs, on-prem networks, and internet
  * VMs in same subnet
  * between VMs in different subnets in same virt net
  * data flow from VMs to Internet
* packets matched to routes by destination
  * ip
  * vnet gateway
  * Virt applicance
  * internet

## User defined routes
* UDR
* do something different
* like routing packets through a VM
* each route can be assoc to mult subnets
* but subnet can only be assoc to single route table
* no charge for routes

### attribs
* route name
* addr prefix
* next hop type
  * vn gw
  * vnet
  * internet
  * virt applicance
  * none

### assoc
* assoc pub subnet w new routing table
* subnet
  * 0-1 route tables
  * name
  * addr range
  * NAT gateway
  * NSG
  * ***Route Table***

## Endpoint uses
* Service traffic from a vnet uses pub IP as source IPs
* w service endpoints, traffice from vpn to service vnet private ips as the source
* allows access to services w/o need for reserved IP addresses and firewalls

### Why
* improved sec
  * secure the service to the vnet
  * no pub IPs used or exposed
  * add virt network rule to allow
* optimal routing for azure service traffic from vnet
* endpoints always take svc traffic directly from vnet to service on azure backbonenet
* simple / less mgmt overhead

### Add svc endpoint
* service
  * azure storage
  * azure sql database, azure sql data warehouse
  * azure db postgresql and mysql
    * extend private addr space of vnet to the azure svc
  * available where db svc avail
  * azure cosmos db
    * conf azure cosmos account to allow access from specific subnet of vnet
    * then, cosmos side limitations can be restricted to only allowing from that subnet, etc
  * azure key vault
    * allo restrict access to specified vnet. also restrict to live of IP v4 ranges
  * azure service bus and azure event hubs
    * enables sec access to messaging from workloads like Vms. traffic secured on both ends

## Private Link uses
* private connectivity to svcs on azure
  * global 
  * no regional restrictions
  * traffic stays on MS network
  * simplifynetwork arch
  * secures traffice between endpoints
* integ with on-prem and peered networks
  * access over privating peering or VPN tunnels
* prot against data exfiltration for azur resources
  * priv link to map private endpoints to azure PaaS resources
  * only mapped resources accessible
* svcs delivered directly to customers' virtual networks
  * works across AD tenants
  * can connect/consume Azure PaaS, MS Partner, and own services in vnet on azure