- [Azure VMs](#azure-vms)
  - [Skills](#skills)
  - [Learning Objectives](#learning-objectives)
  - [General](#general)
  - [Planning](#planning)
    - [Start with the network](#start-with-the-network)
    - [Name the VM](#name-the-vm)
    - [Decide the location for the VM](#decide-the-location-for-the-vm)
    - [Determine the size of the VM](#determine-the-size-of-the-vm)
    - [Understanding the pricing model](#understanding-the-pricing-model)
    - [Storage for the VM](#storage-for-the-vm)
    - [Select an operating system](#select-an-operating-system)
    - [Pricing options](#pricing-options)
# Azure VMs

## Skills
* move VMs between RGs
* manage VM sizes
* add data disks
* config networking
* redeploy VMs


## Learning Objectives
* create VM planning checklist
* Determine VM loc and pricing models
* Determine correct sizing
* Configure VM storage

## General
* IaaS
* provide more control
* VMs provide
  * OS
  * storage
  * networking capabilities
* business scenarios
  * test and dev
  * website hosting
  * storage/backup/recovery
  * high-perf computing
  * big data analysis
  * extended data center

## Planning
* Start with the network
* Name the VM
* Decide the location for the VM
* Determine the size of the VM
* Understanding the pricing model
* Storage for the VM
* Select an operating system


### Start with the network
* Virt networks 
  * VM <-> azure services
    * by default, no access
  * VMs can access one another on same virt network
  * 
### Name the VM
* limit
  * win: 15
  * lin: 64
* convention 
  * (suggested)
    * env
    * loc
    * inst#
    * product or service
    * role
      * sql,web,messaging
  * ex: devusc-webvm01
### Decide the location for the VM
* must select a region.
* resources : cpu, storage, etc
* close to users
### Determine the size of the VM
### Understanding the pricing model
### Storage for the VM
### Select an operating system

### Pricing options
* compute costs
  * priced per hour
  * billed per minute
  * hour price
    * OS
      * if win, license cost
    * VM Size
      * type
        * general
          * balanced
          * testing and dev
          * small to medium db
          * low - medium traffic web servers
        * compute opt
          * medium traffice web server, network appliances, batch processes, app servers
        * memory opt
          * relational db servers, med-lg cache, in-mem analytics
        * storage opt
          * high disk throughput and IO
          * big data, sql, nosql dbs, dw, large trans db
        * GPU
        * High perf compute
          * optional high throughput network intefaces RDMA
    * stop & deallocate - no further charges
  * Resizing
    * current HW config allowed in new size?
* storage costs
  * consuming based
  * reserved VM instances (RI)
    * advanced purchased
    * 1 vm, in a region, 3 years
