- [Azure Virtual Peer Networking](#azure-virtual-peer-networking)
  - [general](#general)
  - [uses](#uses)
  - [Benefits](#benefits)
  - [Determine gateway transit and connectivity](#determine-gateway-transit-and-connectivity)
  - [Create virt network peering](#create-virt-network-peering)
  - [Service chaining](#service-chaining)
    - [uses](#uses-1)
    - [user def routes and service chaining](#user-def-routes-and-service-chaining)
    - [Conn check](#conn-check)
# Azure Virtual Peer Networking

## general
* use to connect to virt networks so they can talk
* allows connectivity w/o exposing services to internet

## uses
* Regional VNet Peering
  * AZ Gov cloud region only allows pairing virt networks in same region
* Global VNet peering
  * mult regions
  * can exist in any azure pub cloud region or china, but not Gov region
    
## Benefits
* priv
* perf
* comm
* seamless
* no disruption

## Determine gateway transit and connectivity
* config VPN Gateway in peered virt network as transit point
* use remote gateway to gain access to other resources
* virt network - only one gateway
* gateway transit supported for VNet peering and Global vnet peering

Allow gateway transit 
* allows comm to resources outside peering
* subnet gateway could
  * use site to site VPN
  * use Vnet to vnet to conn to another virt network
  * use point to site VPN to connect to a client
* NSGs can be applied in virt network to block access to other virt networks or subnets
* virt network peering - open or close the NSG rules between virt networks

## Create virt network peering
1. create 2 virt networks
2. peer virt networks
3. create vms in virt networks
4. test comm
5. configure
   1. peering link name
   2. traffic to remote virt network    
      1. allow/block
   3. traffic from remote virt network
      1. allow/block
   4. virt network gateway
      1. use this virt network's gateway
      2. use remote virt network's gateway
      3. none
   5. remote virt netwok peering link name

## Service chaining
### uses
* VNet Peering nontransitive
  * VNET1 <-> VNET2
  * VNET2 <-> VNET3
  * VNET1 xxx VNET3
* but user-defined routes and service chaining allow transitivity.
  * impl multi level hub and spoke
  * overcome limit on # of VNET peerings per virt network

### user def routes and service chaining
* virt network peering - allows net hob in user def route to be IP of a VM in the peered virt network or VPN gateway
* service chaining lets define user routes  
  * direct traffice from one vnet to virt appliance/network gateway

### Conn check
* status
  * initiated
  * connected
  * 