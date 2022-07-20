- [Azure VPN Gateway](#azure-vpn-gateway)
  - [Use case](#use-case)
  - [Types](#types)
  - [x](#x)
  - [Site-to-site](#site-to-site)
    - [create gateway subnet](#create-gateway-subnet)
    - [Create VPN Gateway](#create-vpn-gateway)
      - [vpn type](#vpn-type)
      - [Gateway sku and gen](#gateway-sku-and-gen)
    - [Create local network gateway](#create-local-network-gateway)
    - [Setup on prem VPN Gateway](#setup-on-prem-vpn-gateway)
    - [Create VPN Conn (in Azure)](#create-vpn-conn-in-azure)
# Azure VPN Gateway

## Use case
* connect data center or lg regional facilities to azure
* or send enc traffic between Azure virt networks over MS Network
* virt network can only have 1 VPN gateway
  * mult connections to share same VPN gateway
  * all vpn tunnels share same avail gateway bandwidth
* can be deployed in azure availability zones
  * bring resiliency scalability hgher avail to virt network gateways
  * phys and logically separate gateways within a region
  * protect on-prem network connectivity to azure from zone level failures

## Types
* site to site
  * on prem data center to azure virt network
* VNet to VNet
  * vnets connected
* Point to Site (User VPN)
  * conn from individual devices to azure virt networks

## x
* virt network gateway -
  * two+ VMs on specific subnet you create called Gateway subnet
  * Virt network gateway VMs contain rouring tables and run specific gateway svcs
  * can't dir config VMs part of virt network gateway


## Site-to-site
* azure
  * create VNets and subnets
  * Specify DNS Server (Optional)
  * create gateway subnet
  * create vpn gateway
  * create local network gateway
* on-prem
  * configure VPN Device
* azure
  * create the vpn conn

### create gateway subnet
* Name it: GatewaySubnet
* contains Ips used by virt network gateway
* create with CIDR block /28 or /27 to accomodate furture reqs
* Gateway VMs deployed to gateway subnet and configured w required VPN gateway settings

### Create VPN Gateway
* VPN Gateway settings 
  * instance
    * name
    * region
    * gateway type:  VPN/ExpressRoute
    * VPN Type: Route-based, policy-based
    * SKU
    * Generation
    * Virt network: 
      * only listed: virt networks in current sub and region
    * Enable active-active mode 
      * disabled
    * Configure BGP ASN
      * disabled
* you can view the IP of the gateway

#### vpn type
* Route based
  * IP forwarding or routing table, direct packets into corresponding tunnels
  * policy / traffic selector is any to any (wild cards)
* Policy based
  * through IPSec tunnels
  * based on IPsec policies
    * combinations of address prefixes between on-pre and VNet
    * policy/traffic selector: access list in VPN dev config
    * limits
      * only basic gateway SKU
      * only one tunnel 
      * Policy0based VPNs for S2S conn, only for certain configs

#### Gateway sku and gen
* specify SKU
* based on 
  * workloads
  * throughput
  * features
  * sla


Policy based - only Gen 1

Route based: also gen 2
SKU VPNGw4 and 5 only for route based

***range is***
* 30-100 max S2S/Vnet to vnet tunnels
* 250 to 10000 P2S IKEv2 conn
* 650 Mbps to 10 Gbps aggregate throughput benchmark


### Create local network gateway
* typically local network gateway at on-prem loc
* give it a name for azure to refer to it
* spec pub IP or FQDN of on-prem VPN device 
* spec IP address prefixes (loc on on-prem net) routed through VPN gateway to VPN device

### Setup on prem VPN Gateway
* use std VPN device, found in list: cisco, Juniper, Ubiquiti, Baracuda etc
* shared key
* pub IP of VPN Gateway

### Create VPN Conn (in Azure)
* add conn
  * name
  * conn type (site to site for ex)
  * virt network gateway
    * vng01 ex
  * local network gateway
    * azure-to-onprem ex
  * shared key (PSK)
* choose locla network gateway
* verify VPN conn
