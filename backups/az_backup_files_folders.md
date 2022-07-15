- [AZ Backups intro](#az-backups-intro)
  - [Skills](#skills)
  - [Learning obj](#learning-obj)
  - [Benefits](#benefits)
  - [Backup center](#backup-center)
    - [Setup recovery svc vault backup options](#setup-recovery-svc-vault-backup-options)
    - [on-prem file folder backups](#on-prem-file-folder-backups)
    - [Manage azure recovery services agent (MARS agent)](#manage-azure-recovery-services-agent-mars-agent)
# AZ Backups intro
## Skills
* create recovery services vault
* create/config backup policy
* perf backup and restore ops - Azure Backup
* configure and review backup reports

## Learning obj
* features/use cases
* config Recovery Svcs Vault backup options
* impl on-prem file and folder backup
* Conf MS Azure Recovery Services Agent

## Benefits
* offload on-prem backup
* backup azure Iaas VMs
* unlimited data transfer
* keep data secure
  * data encryption
    * transmission
    * storage
* get app consistent backups
* retain short/long-term data
* auto storage mgmt
* multiple storage options
  * LRS
  * GRS

## Backup center
* single unified mgmt experience
* gov, mon, op, analyze
* features
  * single pane to mng backups
  * datasource centric mgmt
  * connected experiences
    * uses 
      * azure workbooks
      * azure monitor logs


### Setup recovery svc vault backup options
* recovery svcs vault - storage entity
* set
  * where workload runs
  * what to backup
    * vm, fs, sql server, SAP hana , etc
    * on-prem
      * files and folders
      * and a lot more
* 1 sub
  * up to 25 recovery service vaults per region

### on-prem file folder backups
* backup agent deployed on windows server vm or phys mahcine
* steps
  1. create recovery svc vault
  2. download agent and cred file
  3. install/register agent
  4. config backup

### Manage azure recovery services agent (MARS agent)
* backup files folders on phys or vm
* no sep backup server
* not app aware
  * backup and restore content

