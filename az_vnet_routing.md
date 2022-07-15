- [Az Vnet Routing](#az-vnet-routing)
  - [general](#general)
  - [VPN Gateway](#vpn-gateway)
  - [vnet service endpoint](#vnet-service-endpoint)
  - [Custom routes](#custom-routes)
  - [User Defined Routes (UDR)](#user-defined-routes-udr)
  - [Border gateway protocol (BGP)](#border-gateway-protocol-bgp)
  - [route sele and priority](#route-sele-and-priority)
# Az Vnet Routing 

## general
* can setup sec perim around resources
* control flows in/out of vnet
* restrict access to only allow trafic from trusted srcs


* all subnets have this


|addr prefix|next hop type|
|-|-|
|uniqe to vnet|vnet|
|0.0.0.0|internet|
|10.0.0.0/8|None|
|172.16.0.0/12|None|
|192.168.0.0/16|None|
|100.64.0.0/10|None|

* UDR - User Defined routes
  * can be config to route traffic through an NVA or Azure VPN gateway


## VPN Gateway
* can send 
  * enc traffic Azure <->on-prem over internet
  * encrypted traffic between azure networks

## vnet service endpoint
* extends private addr space in azure
* direct connection to azure resources
* restricts flow of traffic
* VMs can access storage account directly via priv addr space, and deny access from a pub VM
* azure creates routes in route table to direct, as vnet service endpoints created

## Custom routes
## User Defined Routes (UDR)
* udr can override default system routes
  * ex: send traffice through firewall or NVAs
* next hop types
  * Virtual appliance
    * typically fw device, analyze/filter traffice enter/leave network
    * priv IP addr of NIC (on VM) so ip forwarding can be enabled, or provide priv ip of internal LB
  * virtual network gateway
    * routes for specific addr to be routed to Virt network gateway
  * virtual network
    * overrides default sys route within vnet
  * internet
  * none

## Border gateway protocol (BGP)
* nw gateway on prem can exchange routes w virtual network gateway (azure) 
* std routing proto. exchange routing info among 2+ networks
* xfer data and info between diff host gateways
* typical use
  * connected to azure datacenter through azure expressroute
  * also BGP if connect to an azure virtual network using VPN site to site

## route sele and priority
* priority
  1. UDR
  2. BGP
  3. System routes