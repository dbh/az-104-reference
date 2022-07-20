- [Azure Windows VMs](#azure-windows-vms)
  - [Creation](#creation)
  - [background](#background)
  - [Sizing](#sizing)
  - [Mapping storage to disks](#mapping-storage-to-disks)
  - [Unmanaged vs Managed disks](#unmanaged-vs-managed-disks)
  - [Network comm](#network-comm)
  - [Planning network](#planning-network)
# Azure Windows VMs

## Creation
* portal, CLI, PS, or ARM template
* azure marketplace has pre-configured images

## background
* VM 
* azure storage account to hold VHDs
* virtual disks to hold OS, apps, data
* virtual network
  * vm to azure services
* network int <-> VNet
* public ip to access VM (Optional)

## Sizing
* quote limits based on description
* classic
  * 20 virt cores within a region
* storage options
  * SSD
    * std
    * premium
      * intensive I/O mission critical sys fast data processing

## Mapping storage to disks
2 VHDs by default for Windows VM
1. OS. C, 2 GB
2. Temp disk , temp storage for OS or apps, d, sized based on VM size
   1. not persistent
3. Recommend
   1. create dedicated data disks, <=32 GB each

## Unmanaged vs Managed disks
* unmanaged
  * cust responsible for storage accounts for VHDs, for VM disks
  * storage account rates for amount of space used
  * storage account limit of 20,000 I/O op per sec.  or 40 Std VHDs full throttle
* managed
  * newer option
  * recommended
  * Azure managed storage accounts
  * spec
    * disk type
    * size
  * don't wory about storage account limits
  * inc reliability
  * better security
  * snapshot support
  * backup support

## Network comm
* VM comm w external resources via virt network (VNet)
* priv network in single region for resources 

## Planning network
* create a new one
* join an existing one
