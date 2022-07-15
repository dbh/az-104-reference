- [Azure backup VMs](#azure-backup-vms)
  - [options](#options)
    - [managed disk - snapshots](#managed-disk---snapshots)
    - [Managed disk - images](#managed-disk---images)
    - [azure backup](#azure-backup)
    - [azure site recovery](#azure-site-recovery)
  - [vm backup/restore](#vm-backuprestore)
  - [Azure Backup Server](#azure-backup-server)
  - [azure storage - manage soft delete](#azure-storage---manage-soft-delete)
  - [azure site recovery](#azure-site-recovery-1)
# Azure backup VMs
* regular intervals
## options
### managed disk - snapshots
* dev and test
* disk snapshots for Vms using Managed disks
* read-only, full copy of managed disk
* billed based on used size (not provisioned size)
* no awareness beyond disk on which snapshot occurred. 
* doesn't work/consider striping or multiple disks
* phases. Recovery job complete after both phases
  * take snapshot
  * send to data vault
* snapshots taken locally. reduce backup/restore time.
  * retention value 1-5 days
* up to 32 TB
* Supports all HDD and SSD
* incremental snapshots as pag eblobs
* unmanaged drives -> data stored in local storage account.
* premium
  * snapshots for isntant recovery points in in the 10 tb limit of allocated space
  * config snapshot retentionm based on restore needs
### Managed disk - images
* create managed custom image from a VHD in storage account or directly from VM
* can create many VMs based on these images
### azure backup
* VMs running prod workloads
* app consistent backups, win, linux VMs
* recovery points stored in geo redundant recovery vaults
* recover whole Vm or files

### azure site recovery
* prot Vms from major disaster, when whole region has outage
* can be configured for Vms
* Recovery in mater of minutes


## vm backup/restore

1. create recovery services vault
   * in region where you want data stored
   * replication: LRS or GRS (default)
2. use portal to define backup
3. backup the VM

* agent must be installed on the VM in order to backup the files/folders


## Azure Backup Server
* another way to backup VMs
* Data Protection Manager (DPM) or MS Azure Backup Server (MABS). 
  * specialized workloads, VMs, files, folders, volumes, incl sharepoint, ex, sql server
  * app aware backups for common apps
  * machine state backups : 
    * bare-metal
    * system-state
  * on-prem
    * each machine runs DPM/MABS prot agent., 
    * don't need MARS agent on individual stations
  * manage backups for mult machines gathered into groups in single console

|Comp|benefit|limit|prot|where stored|
|-|-|-|-|-|
|Azure Backup (MARS) agent|backup files/folders on phys or win VM. no sep backup server required| 3x per day. not app aware.|files/folders|recovery services vault|
|Azure Backup server (MABS)|app aware. flex on when to backup; recov granularity. linux. Hyper V and VMWare Vms; backup/restore VMWare VMs. doesn't require system center license|No oracle workloads. requires live azure sub. no support for tape|File,folder,vol, VMs, apps, workloads.|recover services vault, locally attached disk|

## azure storage - manage soft delete
* for blobs
* for VMs backups
* 14 days in soft-delete state

## azure site recovery
* cross regions
* availability sets
* bus. continuity .
* keeps bus apps/workloads running during outage
* fail over from primary to secondary region

* replication Scenarious
  * replicate azure VMs from one azure region to another
  * replicate on-prem VMWare VMs, hyper-v VMs, phys servers (win/linux), Azure Stack VMs to azure
  * AWS WIndows instances to azure
  * on-prem VMWare VMs, Hypver-V VMs (sys center VMM), phys servers over to 2nd site
  
* features
  * setup/manage replicaiton,failover, failback
  * elim cost/complexity of maintaining 2nd datacenter
  * orchestrates replication w/o intercepting app data
  * continuous replication for Azure Vms / VMWare VMs,  30 sec or greater
  * can replicate using recovery points w app consistent snapshots
  * run planned failovers for expeted outages . zero data loss. no unplanned failover. etc

site recovery integrates with azure. reserving IPs, config LBs, integ azure traffic manager