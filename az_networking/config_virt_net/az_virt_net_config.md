- [Azure - Virtual Network configuration](#azure---virtual-network-configuration)
  - [Example stuff to move over](#example-stuff-to-move-over)
  - [Impl](#impl)
  - [Create](#create)
    - [Plan IP addressing](#plan-ip-addressing)
    - [Static vs Dymamic](#static-vs-dymamic)
    - [Create public IP addressing](#create-public-ip-addressing)
    - [Assoc pub IP](#assoc-pub-ip)
    - [Assoc private IP](#assoc-private-ip)
# Azure - Virtual Network configuration

## Example stuff to move over
* Virtual network
* Load Balancer
* Application Gateway
* traffic Manager profile
* Virtual network gateway
* Virtual WAN

## Impl
* rep of own network in cloud
* logical isolation of azure cloud 
* VNets - 
  * provision/manage VPNs
  * link VNets w other VNets
  * link VNets with on-prem infra (hybrid / cross premises solutions)
* each VNet has own CIDR block
* can be linked to other 
    * VNets
    * on-prem networks
  * as long as no CIDR overlap
* control DNS server settings for VNets,
* seg into VNet subnets
* Create dedicated priv cloud only VNet
* extend data center w VNets
  * S2S VPNs
* Enable hybrid 

## Create
* vnet can be segmented into subnets
* consider
  * service requirements    
    * svc may require and even create it's own subnet
  * virtual appliances
    * override azure default routing to prevent azure routing between subnets or a specfic route to go through an network virtual appliance (NVA)
  * service endpoints
    * can limit azure resources to specific subnet w vnet endpoint
      * can deny access to resources from internet
  * net seg groups (NSG)
    * assoc 0+ NSGs to each subnet in vnet
  * private links
    * azure private link - provide connectivity from vnet to azure platform as service (PaaS), customer owned, or MS Partner services.  Eliminates exposure to pub internet
* restricted IP addr
  * x.x.x.0 network address
  * x.x.x.1 default gateway
  * x.x.x.2, x.x.x.3: Reserved by azure to map Azure DNS IPs to VNet space
  * x.x.x.255: Broadcast

### Plan IP addressing
* private IP addr
* Public IP addr

### Static vs Dymamic
* Static best for
  * DNS resol
  * IP addr based sec models
  * TLS/SSL certs
  * Role-based VMs like Domain controllers and DNS Servers

### Create public IP addressing
* IPv 4, 6, or both
* SKU - has to match SKU of LB 
  * basic
  * std
* name
* assignment
  * dyn
    * stays same if VM is rebooted or stopped (but not delloc)
    * released when pub IP dissasoc from resource
  * static
    * if IPv6 selected, assignment must be Dyn for basic SKU, Std SKU addresses static for both ipv 4 and 6

### Assoc pub IP
|pub ip addr|ip addr assoc|dyn|static|
|-|-|-|-|
|VM|NIC|Yes|Yes|
|LB|Front-end conf|Yes|yes|
|VPN Gateway|Gateway IP conf|Yes|Yes*|
|App gateway|front-end conf|Yes|Yes*|
\* Static IP only avail on certain SKUs

Address SKUs
|Feature|Basic SKU|Std SKU|
|-|-|-|
|IP Assign|either|static|
|Sec|open by default|secure by default|
|resources|Network int, VPN gateway, app gateway, internet facing LB|network int, pub std LB|
|Redundancy|not zone redundant|zone redundant by default|

### Assoc private IP
|pub ip addr|ip addr assoc|dyn|static|
|-|-|-|-|
|VM|NIC|Yes|Yes|
|Internal LB|front-end conf|Yes|Yes|
|App Gateway|front-end conf|Yes|Yes|

* Dynamic
  * next sequential ip avail
* Static
  * you select. in subnets addr range
