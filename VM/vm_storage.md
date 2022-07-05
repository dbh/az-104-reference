- [VM Storage](#vm-storage)
  - [Data disks](#data-disks)
  - [Virtual machine storage options](#virtual-machine-storage-options)
  - [Managed disks](#managed-disks)
# VM Storage

* all VMs have at least 2 disks
  * OS (win OS sometimes)
    * pre-installed
    * registered as SATA drive
    * C (win) by default
  * temporary disk
    * d (win) by default
    * /dev/sdb  mounted to /mnt
  * possibly others
* stored as VHDs

## Data disks
* managed disk attached to VM to store appd ata
* other data need to keep around
* reg as SCSI drives
* labeled w letter of choice
* size of VM limits 3 of data disks and storage types to host disks

## Virtual machine storage options
* azure premium storage
  * high perf
  * low latency
  * for IO intensive workloads
  * SSDs
  * existing VM disks can be migrated

## Managed disks
* a VHD
* "managed" - abstraction over page blobs, blob containers, azture storage accounts
* ~ similar to phys disk
* virtualized
* stored as page blobs
* random IO storage object in azure
* types
  * Ultra Solid State Drives (SSD)
  * Premium SSD
    * recommended when high IOPS
  * Standard SSD
  * Standard Hard disk drives (HDD)