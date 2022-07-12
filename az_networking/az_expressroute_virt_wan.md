- [Azure ExpressRoute and Virtual WAN config](#azure-expressroute-and-virtual-wan-config)
  - [General](#general)
  - [ExpressRoute](#expressroute)
    - [Benefits](#benefits)
  - [Coexist site-to-site and ExpressRoute](#coexist-site-to-site-and-expressroute)
    - [Connection models](#connection-models)
    - [Compare](#compare)
  - [Virtual WAN](#virtual-wan)
# Azure ExpressRoute and Virtual WAN config

## General
* extend  on-prem networks into MS Cloud
* on-prem
  * partner edge
    * primary conn
      * Microsoft Edge
        * Office 365, CRM, VNets, Apps
    * secondary con
      * ...

* Makese conns fast, reliable, private
* private conn between azure data centers/infra and on-premn

* estab conn to azure at 
  * express route loc
    * exchange provider facil
  * from existing WAN network
    * (multiproto label switching (MPLS) VPN) 

* virt priv cloud for
  * storage, backup, recovery
  * up to 100 Gbps

* Extend and connect data centers
* build hybrid apps

## ExpressRoute

* express Route supported all regions/locs
* Express Route Locations
  * where MS peers w several svc providers

### Benefits
* layer 3 conn . MS uses BGP to exchange routes between on-prem network, Azure, and MS Pub addresses
  * BGP routes created for diff traffic profiles
* Redundancy
* Connectivity to MS CLoud services
  * ER circuit , 2 conn to MS Enterprise edge routers
  * MSEE
  * conn provider/your network edge
  * MS requireds dual BGP conn from conn provider/network edge to each MSEE
* Connectivity to all regions in geo politicla region
* Global conn w ExpressRoute premium add-on
  * go past geo political boundaries
* across on-prem conn w ExpressRoute Globala Raech
  * across on-prem sites, via ExpressRotue circuits
    * ex  Silicon valley, texas, etc
    * data between those goes across MS network
* badwidth options
  * purchase
* flex bill

## Coexist site-to-site and ExpressRoute
* direct, priv conn from your WAN to MS
* Site-to-Site VPN traffic travels encrypted over pub internet
  * as a fail-over path for ExpressRoute
  * 2 Virt Net gateways for same virt network
* both above, configured for same Virtual Network

### Connection models
* colo at cloud exchange
  * colo in a facil w cloud exchange
  * order virt cross-connections to MS Cloud
  * Layer 2 cross conn or managed Level 3 cross conn
* pt-to-pt ethernet
  * on prem data center/offices to the MS Cloud through pt-to-pt ethernet links
  * l2 or managed l3 conn <-> MS Cloud
* Ant to any (IPVPN) networks
  * integration your WAN w MS Cloud
  * IPVPN providers (MPLS) VPN offer any-to-any conn between your branch offices and data centers
  * MS CLoud can be interconn w WAN , appears as a branch office

### Compare
|Conn|Az svcs|bandwidths|proto|use cases|
|-|-|-|-|-|
|Vnet, pt-to-site|Azure IaaS svcs, Az VMs|gw SKU|active/passive|dev test , lab env|
|vnet, site-to-site|Azure IaaS svcs, Az Vms|<= 1Gbps agg|active/passive|dev/test/lab env. small prod, VMs|
|ExpressRoute|Azure IaaS and PaaS svcs, MS365|50-100 Gbps|active/active|Ent class mission crit workloads. Big data|

## Virtual WAN
