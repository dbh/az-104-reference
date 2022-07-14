# Az Ip Addr Schema

## General
* good strategy 
  * provide flex
  * room for growth
  * integ with on-premise networks
* priv ip capa
* pub ip capa
* ident requirements for ip addressing re integ on-prem network

## understanding of components in a network
* Routers
* firewalls
* switches
* network segmentation
* perimeter network (sim to DNZ IMO)

## non-routable IP ranges for internal networks
* 10.0.0.0 to 10.255.255.255
* 172.116.0.0 to 172.31.255.255
* 192.168.0.1 to 192.168.255.255

* num subnets dependent on CIDR blocks
  * Classless Inter-Domain Routing

## Azure Ip addressing
* vnets use private Ip (duh)
* ranges of private IP addr, same as for on-prem Ip addressing
* admin has full control over ip address assignment, DNS, sec settings, sec rules in Azure vnet
* admin ccan add/remove subnets dep on CIDR

## Azure network design comps
* vnets
* subnets
* NSGs
* firewalls fw
* load balancers lb

## Pub/priv addressing in azure
### Types
* pub
* priv

### allocation
* dynamic
* static

* SKUs
  * Both Basic and Std
    * default inbound originated flow. idle timeout 4 min, up to 30
    * fixed outbound originated flow idle time of 4 min
  * Basic
    * open by default
    * NSG optional but recommended
    * avail for inbound traffic only
    * avail when using instance meta data service (IMDS)
    * No Avail Zone support
    * No routing prefs
  * Std (by default)
    * always static alloc
    * secure, closed to inbound. enable w NSG
    * zone redundant
    * optionally zonal
    * can be assigned to network interfaces, std pub LB, app gw, vpn gw
    * can be used w routing prefs
    * can be used as anycast FE IPs for cross-region LBs


## Pub IPs 
### Dyn
* dynamic pub IPs, can change, allocated on creation on start of VM
* released on stop/delete
* alloc within regional unique pool
* default
### Static
* won't change obv
* released only on delete of resource or manual change to IP alloc

## Pub IP addr prefix
* from pool of avail addr
* unique to each region
* assigned from pool
* avail zones
  * pub ip addr prefix can be created as zone redundant or assoc w an avail zone
* Can specify fw rules for known range of IPs
  * ex: data centers in diff regions

***prefix size***
* IPv$ or IPv6
* tech like Azure traffic manager to balance region specific instances
* cannot bring own IP
* cannot spec address when create prefix. Comes from azure pool. 
* pub ip canot be moved between regions

## Private IPs
* dynamic private
  * DHCP lease
  * can change
* static private - 
  * DHCP reservation
  * persists if resource is stopped or deallocated

ranges
* 10.0.0.0/8
* 172.16.0.0/12
* 192.168.0.0/16

cannot use
* 1st three addresses
* first IP
* last IP