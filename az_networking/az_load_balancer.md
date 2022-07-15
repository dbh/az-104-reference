- [AZ Load Balancer](#az-load-balancer)
  - [general](#general)
  - [Impl](#impl)
    - [Public](#public)
    - [Internal](#internal)
  - [SKU determination](#sku-determination)
  - [Backend pools](#backend-pools)
    - [SLA w](#sla-w)
    - [Avail set](#avail-set)
    - [Avail zone](#avail-zone)
  - [Balancer rules](#balancer-rules)
  - [Also](#also)
    - [Health probe](#health-probe)
  - [Configure a pub LB](#configure-a-pub-lb)
    - [Distrib modes](#distrib-modes)
  - [LB and Remote Desktop Gateway](#lb-and-remote-desktop-gateway)
  - [LB and media upload](#lb-and-media-upload)
# AZ Load Balancer

## general
* LB rules determine how traffic distrib to Backe end
* health probes
* health balancing rules

![Diagram](https://docs.microsoft.com/en-us/learn/wwl-azure/configure-azure-load-balancer/media/load-balancer-4caf947b.png)

## Impl
### Public
* map pub IPs and port #s of incoming traffic to private Ips and port numbers of VM
* Map also response traffic from VM
### Internal
* dir traffic to resources inside VNet or that us VPN 
* FE IPs and vnets never exposed to internet endpoint
* enables
  * within vnet - LB from VMs to another set of VMs
  * cros-premises vnet
  * LB from on-prem computers to set of VMs in vnet
  * mult-tier apps
    * lb for internet facing multi-tier apps
    * backend tiers not internet facing
    * backend tiers req traffic LB from the internet facing tier
    * LoB apps
      * on-prem servers are in set of computers w LB traffic

## SKU determination
* details
  * name
  * region
  * type
  * SKU
    * std / basic
  * vnet 
  * subnet
  * IP assignment
    * static / dyn

Note
* Std LB recommended
* Basic can be upgraded to Std

Diff
* Basic
  * fewer backend pool instances
  * no HTTP prob, but HTTPS and TCP
  * no avail zones
  * mult front ends - inbound only
  * sec
    * open by default
    * NSG optional
    * vs, closed to inbound, internal traffic from vnet to internal LB allowed
  * no sla vs 99.99
* std
  * https health probes
  * avail zones
  * diagnostics azure monitor
  * HA ports
  * outbound rules
  * 99.99% SLA

## Backend pools

* tier
  * std
    * any VM in single vnet
    * inc blend of Vms, avail sets, VM scale sets
    * up to 1000 instances
  * basic
    * VM in single avail set or VM in scale set
    * up to 300 instances
* config in backend pool blade
  
### SLA w 

|config|SLA|info|
|-|-|-|
|avail set|99.95%|prot from hw fail in datacenter|
|avail zone|99.99%|prot from entire datacenter failure|

### Avail set
* logical grouping
* isolate VM resources from each other when deployed
* azure ensures the VMs are on diff phys servers, rack, storage units, network switches

### Avail zone
* groups one or more datacenters that have independent power,cooling,networking. VMs in avail zone are in diff phys locations within same region.

## Balancer rules
* LB rule defines how traffic distrib to bakend pool
* rule maps given frontent IP / port combo to backend IP addr(s) and ports combo
* health probe


## Also
* LB can be used in conjuction with NAT rules
* session persistence
* 5-tuple hash
  * src ip
  * src port
  * dst ip (Cloud Service VIP)
  * dst port (pub port)
  * proto
* persistence flag
  * none (defuault)
  * Client IP
  * Client IP and Proto

### Health probe
* allow LB to mon status of app
* dyn add  remove VM from rotation 
* settings
  * name
  * proto
  * port
  * path 
  * interval (s)
  * unhealthly threshold (# consec fail)
* HTTP custom probe
  * every 15 sec, by default
  * 200 status within 31 sec means fine
* TCP custom prob
  * successful TCP session to defined port
  * if port listener on VM exists, probe succeeds
* Guest agent probe 
  * no recommended if other methods avail

## Configure a pub LB
* five tuple hash whatever used

### Distrib modes
* source IP affinity
  * sticky/sesion/client IP
  * could use 5 or 
  * 2 tuple hash
    * src ip, dst ip
  * 3
    * src,dst,proto 

* config
  * azure LB
    * LB rules
      * name
      * ip version
      * front end IP
      * proto
      * port
      * backend port
      * backend pool
      * Session persistence
        * None
        * client ip
        * Client IP and protocol

## LB and Remote Desktop Gateway
* Remote Desktop Gateway is win svc
* enable clients on internet to make RDP thru FW to remote desktop servers
* 5 tuplic hash in LB incompatible
* need source IP affinity to work with LB
## LB and media upload
* client init session through TCP (remain connected)
* file upload via UDP
* use source ip affinity