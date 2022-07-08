- [Azure Firewall](#azure-firewall)
  - [General](#general)
  - [Create](#create)
  - [Benefits](#benefits)
  - [use cases](#use-cases)
  - [NAT Rules](#nat-rules)
  - [Network rules](#network-rules)
  - [App rules](#app-rules)
  - [Rule processing](#rule-processing)
# Azure Firewall

## General

* managed
* cloud-based
* net sec service
* protect Azure Virtual Network resources
* statefull as svc
* high avail
* scalability


features
* high avail
* avail zones
  * config during deployment. span mult avail zones
* unrestricted cloud scalability
* application FQDN filtering rules
  * limit outbound HTTP/S traffice or Azure SQL Traffice to specificed list of FQDNs incl wild cards
* network traffic filtering rules
* threat intelligence
* mult pub ip addresses

## Create

* virt hub
  * act as centrla point of connectivity to your on-premise network
* spokes
  * virt networks, peering w hub
  * can be used to isolate workloads
* Traffic
  * on-premises datacenter <-> (ExpressRoute || VPN Gateway) <-> hub 

## Benefits
* cost savings. shared resources for mult workloads
  * network virt appliances (zs), DNS servers, single loc
  * bypass sub limits (peer virt networks from diff subs to central hub)
  * separations of concerns between SecOps, InfraOps, and   workloads (DevOps)

## use cases
* workloads in dif env share services
  * ex: dev and test env shares DNS server
  * each env goes into spoke for isolation
* workloads don't require connectivity to each other, but require shared services
* Enterprises require control over security aspects

## NAT Rules
* Azure Firewall Destination Network Address Translation (DNAT)
  * translate and filter inbound traffic to subnets
  * NAT rule collections
* Allowing inbound SSH,RDP, non-HTTP/S apps 
* NAT rules require corresponding network rule to allow
* attribs
  * name
  * proto
  * source
  * dest    
    * fw pub ip side
  * dest ports
    * fw pub ip side
  * translated address 
    * IP of svc (VM, internal LB, ...) that priv hosts or presents service
  * translated port
    * port that inbound traffice will be routed by azure fw


## Network rules
* any non-HTTP/s traffice allowed through fw must have network rule
* ex: one subnet must comm w resources in another subnet -> configure network rule from src to dst
* attribs
  * name 
  * proto
  * src
  * dst 
  * dst port

## App rules
* app rules define FQDNs accessible from a subnet
  * ex: specify windows update network traffice through firewall
* attribs
  * name
    * src
    * protocol:port
  * target FQDNs or wildcard(s)
    * FQDN tag reps group of FQDNs assoc w well known MS Services
    * ex: 
      * Windows Update
      * App service environment
      * azure backup

## Rule processing
* network rules
* app rules (network and app)