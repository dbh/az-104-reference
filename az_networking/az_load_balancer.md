- [AZ Load Balancer](#az-load-balancer)
  - [general](#general)
  - [Impl](#impl)
    - [Public](#public)
    - [Internal](#internal)
  - [SKU determination](#sku-determination)
  - [Backend pools](#backend-pools)
  - [Balancer rules](#balancer-rules)
  - [Also](#also)
    - [Health probe](#health-probe)
# AZ Load Balancer

## general
* LB rules determine how traffic distrib to Backe end
* health probes
* health balancing rules

![Diagram](https://docs.microsoft.com/en-us/learn/wwl-azure/configure-azure-load-balancer/media/load-balancer-4caf947b.png)

## Impl
### Public
* map pub IPs and port #s of incoming traffice to private Ips and port numbers of VM
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