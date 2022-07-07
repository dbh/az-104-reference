- [AZ VM Win Ports](#az-vm-win-ports)
  - [Steps](#steps)
  - [NSG](#nsg)
    - [Setup rules](#setup-rules)
# AZ VM Win Ports
* apps can make outgoing requests

## Steps
1. create NSG
2. create inbound rule allowing port 20,21 FTP

## NSG
* VNets foundation azure network model
* isolation and prot
* main tool to use to enforce / control net traffice rules
* NSGs provide a sw fw
* SGs can be assocate to a network interface or subnet 

### Setup rules
* all allowed by default
* priority order, lowest 1st
* deny stops the eval on match
* last rule, deny all
* allow rule
* deny rules
* inbound
  * subnet
  * then network int
* outbound
  * network int
  * then subnet