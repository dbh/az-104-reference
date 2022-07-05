# Az Azure Files And Sync

* file / doc sharing
* diff geo regions for office
* azure files - central loc for documents
* config Azure File Sync to keep info sync across mult office
* access anywhere
* lift/shift
* azure File Sync  - 
  * azure file shares can be synced with WIndows Servers (in cloud or on-prem) - distrib caching etc
* shared apps
* diag data
* tools and utils
* 

|feature|desc|when|
|-|-|-|
|azure files|SMB,NFS,client libs, REST|lift and shift. Access files/data from mult VMs etc|
|azure blobs|client libs, REST,unstructured data, massive scale|app to support streaming and random access scenarious. app access from anywhere|

Notes
* Replacment for Office file server, SMB, NAS
* SMB protoocl
* mounted servers/volumes
* azure VMs and on-premise apps can access 


## Create new file share
* spec 
  * account
* mapping
  * mount
    * win
    * lin
    * mac ox
  * authentication
    * AD
    * Storage Account Key (admin only access)
* options
  * secure xfer req


## File share snapshots
* Capa for taking share snapshots
* point in time
* read only copy of data
* snapshot at share level
* retrieval of individual files
* incremental
* only have to retain the most recent to restore the share
### when 
* prot against app error and data corruption
* prot against accidental deletions or changes
* general backup

## Implmenet File Sync
* Azure File Sync
* * centralize org's file shares in Azure files
* keep on-prem file server (if you like)
* transforms Windows Server into quick cache of Azure file share
* any win protocol, SMB, NFS, FTPS
* many caches as you want
* scenario
  * lift and shift
  * branch offices
  * backup and DR
  * file archiving

### File sync component

## Storage Sync Service
* top level azure resource for azure file sync
* peer of storage account
* can also work at RG level
* can create sync relationships w mult storage accounts via sync groups
* sub can have mult Storage Sync Services
* sync group
  * define sync topo for set of files
  * endpoints within sync group keep in sync w each other
* Registered Server
  * rep trust between your server/cluster and Storage Sync Service
* Azure File Sync Agent
  * runs on Windows Server
  * syncs w Azure file share
  * components
    * FileSyncSvc
      * background svc - monitor changes on server endpoints, inits sync sessions to azure
    * StorageSync.sys
      * sys filter. tiers files to azure files (when cloud tiering enabled)
    * PowerShell mgmt cmdlets
* Server endpoint
  * rep specific loc on a registered server., ex folder on server volumn
  * mult server endpoints can exist on same vol, if namespaces don't overlap
* cloud endpoint
  * azure file share part ofsync group
  * Azure File share can be member of 1 sync group

## Deploy azure file sync
* Deploy Storage Sync Service   
  * need name, sub, RG, loc
* prep windows server(s)
  * temp disable IE Enhanced Sec
  * ensure latest PS
* Install file sync agent
  * recommend: MS Update running
* Register Windows server
  * Server Reg UI
    * sub id, rg, storage sync service
    * can only reg w 1 storage sync svc at a time

