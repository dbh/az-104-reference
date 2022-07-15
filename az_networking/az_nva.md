- [Azure Network Virtual Appliance (NVA)](#azure-network-virtual-appliance-nva)
  - [features like](#features-like)
  - [General](#general)
    - [UDR](#udr)
  - [NVA in high avail arch](#nva-in-high-avail-arch)
  - [How to install additional packages at creation time for a VM...](#how-to-install-additional-packages-at-creation-time-for-a-vm)
# Azure Network Virtual Appliance (NVA)

## features like
* firewall
* WAN optimizer
* app delivery controllers
* routers
* load balancers
* IDS/IPS
* proxies

## General

* some available in azure marketplace
* could define FW apps into vnet w diff configs
* could put fw appliance in perim network or impl microsegmentation, etc
  * could do all packets at OSI layer 4, 
  * and for app aware appliances layer 7
* NVA acts as router that forwards requests between subnets on vnet
* some NVAs need mult NICs

### UDR
* most env
  * default sys routes already defined by azure are enought to get env running
  * some cases, create routing table and add custom routes like
    * access to internet via on-prem network using forced tunneling
    * using Virt applicances  to control traffic



## NVA in high avail arch
* traffic routed through NVA
* NVA becomes critical to infra
* Make high avail


## How to install additional packages at creation time for a VM... 
* make a file called "cloud-init.xt"
* ex contents
```yaml
#cloud-config
package_upgrade: true
packages:
    - inetutils-traceroute
```
* create the VM, and reference the config file, in --custom-data. ex
```bash
az vm create \
    --resource-group [sandbox resource group name] \
    --name public \
    --vnet-name vnet \
    --subnet publicsubnet \
    --image UbuntuLTS \
    --admin-username azureuser \
    --no-wait \
    --custom-data cloud-init.txt \
    --admin-password <password>
```

watch for VM creation to complete
```bash
watch -d -n 5 "az vm list \
    --resource-group [sandbox resource group name] \
    --show-details \
    --query '[*].{Name:name, ProvisioningState:provisioningState, PowerState:powerState}' \
    --output table"
```

get list of IPs for a VM
```bash
PUBLICIP="$(az vm list-ip-addresses \
    --resource-group [sandbox resource group name] \
    --name public \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"

echo $PUBLICIP
```

and 
```bash
PRIVATEIP="$(az vm list-ip-addresses \
    --resource-group [sandbox resource group name] \
    --name private \
    --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
    --output tsv)"

echo $PRIVATEIP
```

* test routing with ssh and then traceroute from vm

