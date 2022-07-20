- [VM Availability Sets](#vm-availability-sets)
  - [Essential capability](#essential-capability)
  - [How/Create](#howcreate)
  - [SLAs](#slas)
# VM Availability Sets

* logical feature
* ensure group of VMs are deployed so they aren't all subject to single point of failure
* not all upgraded at same time
* VMs in set - identical set of f() and same sw
* ensures running across mult phys services, racks, storage units, network switches

## Essential capability
* redundancy
  * mult VMs in set
* each app tier in separate availability sets
* combine load balancer with availability sets
* use managed disks with the VMs

## How/Create
* Disaster Recovery section, DR recovery section (or ARM Templates), scripting, or API tools
* details
  * name
  * region
  * fault domains (ex 2)
  * update domains (ex 5)
  * use managed disks (yes)

## SLAs
* all VMs w 2+ instances, in 2+ availability zones in same region
  * guarantee VM connectivity to at least one instance, at least 99.99% of time
* all VMs, 2+ instances in same availability Set, 
  * guarantee VM connectivity 99.95%
* Single VM, premium storage on all OS disks and data disks, 
  * guarantee VM Connectivity 99.9%
