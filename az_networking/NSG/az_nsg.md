- [Azure Network Security Groups](#azure-security-groups)
  - [What](#what)
  - [Configure](#configure)
    - [Rule details](#rule-details)
    - [Inbound](#inbound)
    - [Outbound](#outbound)
  - [Determine NSG effective rules](#determine-nsg-effective-rules)
  - [Creating inbound rule](#creating-inbound-rule)
# Azure Network Security Groups

## What
* limit network traffic to resource in virt network
* list of sec rules 
  * allow or deny 
  * inbound or outbound
  * subnet or network interface
* Subnets
  * NSG assigned to subnet - protected/screened subnets (DMZ)
  * each subnet can have >=0 NSGs
* Network interfaces
  * could assign NSGs to a NIC
  * each NIC can have >=0 NSGs
* Associations
  * blades


## Configure
* default rules can be overridden 


### Rule details
* name
* priority
* port
* protocol
* source (any, IP addresses, service tag)
* destination (any, ip addresses, virt network)
* action

### Inbound
* 3 default inbound
  * allow any vnet inbound from same vnet
  * allow any inbound from azure load balancer
  * deny all inbound

### Outbound
* 3 defaults
  * allow all virt network to virtnetwork
  * all any outbound to internet
  * deny all outbound

## Determine NSG effective rules
* NSGs evaluated independently
* any allow rule must exist in both levels or traffic not allowed
  * Subnet level
    * NIC level
* for troubleshooting seem "Effective security rules" link

## Creating inbound rule
* Service - drop down list, or provide own port range
* Port ranges
  * single port, range, CSV, or *
* priority

