- [AZ AKS Storage](#az-aks-storage)
  - [Configure](#configure)
    - [Concepts](#concepts)
  - [Volumes](#volumes)
  - [Persistent volumes (PV)](#persistent-volumes-pv)
  - [Storage classes](#storage-classes)
    - [Default](#default)
    - [managed-premium](#managed-premium)
    - [azurefile](#azurefile)
    - [azurefile-premium](#azurefile-premium)
  - [Persistent volume claims (PVC)](#persistent-volume-claims-pvc)
# AZ AKS Storage

## Configure 

* default storage, goes away w container instance
* some workloads require persisted storage
* mult pods may need to share data 
* or reattach data volume if pod rescheduled on diff node
* or inject sensitive data or app config into pods

### Concepts 
* Volumes
* Persistent volumes
* Storage classes
* Persistent volume claims

## Volumes
* pods ephemeral
* Volume always way to store/retrieve
* traditional
  * backed by azure storage (Disks or Files)
* Azure Disks
  * create Kubernetes DataDisk resource
  * can use Azure Premium storage, back w SSD or Azure Std Storage/HDD
  * Most prod, use Premium storage
  * mount as ReadWriteOnce
    * only available to single node

* Azure Files
  * can mount SMB 3.0 share, backed by azure storage account to pods
  * Std/HDD or Premium/SSDs

## Persistent volumes (PV)
* Volumes regularly disappear after pod goes away
* PV (Persistent Volume) 
* Can be statically created by a cluster admin or dynamically created by Kubernetes API server
* if pod scheduled/moved to another node (or whatever), storage still present
* if pod scheduled and requests storage whcih is not avail, K can create underlying Azure Disk or Files storage and attach it
* Azure Disk or Files choice, usually depends on whether mult pods need to access
* Dynamic provision uses StorageClass to ident azure storage type

## Storage classes
* options
  * tier
    * premium
    * standard
  * reclaimePolicy
* create new storage class type using kubectl
### Default
* StandardSSD to create Managed Disk
* reclaime policy ensures Azure Disk is deleted when persistent volume that is used is deleted
### managed-premium
* Azure Premium storage to create Managed Disk
* same on reclaimPolicy
### azurefile
* std, same on reclaim
### azurefile-premium
* premium, same on reclaim

## Persistent volume claims (PVC)
* PBC requests either Disk or File storage of particular StorageClass, access mode, and size
* K API server can dynamically provision
* pod def incl vol mount once the vol can been connect to pod
* PV bound to PVC once avail storage resource assigned to requesting pod
* 1:1 mapping of persistent volume claims