- [Azure Scale sets](#azure-scale-sets)
  - [Benefits](#benefits)
  - [Create](#create)
- [AutoScale](#autoscale)
  - [Autoscale benefits](#autoscale-benefits)
  - [config](#config)
# Azure Scale sets

* VM scale sets - resource to deploy/manage set of identical VMs
* true autoscale
* no pre-provision required
* easier to build lg scale svcs targeting big compute and big data and containerized workloads
* demand up -> add more VMs
* demand down -> remove VMs

## Benefits
* same os and config
* scale sets support Azure Load balancer
  * basic layer 4 traffic distrib
  * azure app gateway 
    * layer 7 traffic distrib and ssl termination
* can auto scale up/down depending on demand
* up to 1000 Vm insttnces
* if create/upload own custom VM images, limit is 600

## Create
* details
  * init instance count
  * size (ex Standard D2sV3)
  * spot instance (ye/no)
    * low priority VMs allocated from excess compute capacity
    * spot enable several workload types to run at reduced cost
  * use managed disks
    * hide underlying storage accounts and shows abstraction of a disk
  * enable scaling policy
    * no: 100 in one placement group
    * yes: mult placement groups. up to 1000 total capacity
  * Spreading alg:
    * max (recommended)
    * fixed spreading

# AutoScale
## Autoscale benefits
* auto adjust for capacity
* creation of rules for acceptable perf
* scale out
* scale in
* schedule events
  * need a bunch for this special event at a fixed time
* less overhead

## config
* init instance count
* scaling
  * policy
    * manual
    * custom
  * min Vms
  * max VMs
* scale out
  * CPu threshold %
  * duration in min
  * number VMs to inc by
* scale in
  * cpu threshold %
  * number Vms to dec by
