# AZ Storage Tools

## Manage storage
* export from Azure job
* import from Azure job
* install/use Azure Storage Explorer
* Copy data by using AzCopy
* Configure/use
  * Storage Explorer
  * Import/Export service
  * AzCopy

## Azure Storage Explorer
* connect to storage 
  * accts assoc w/ azure subs
  * accts and svcs shared from other azure subs
  * and manage local storage using Az storage Emulator

*  Attached via
   *  External Storage
      *  storage account name, key, endpoints
   *  Storage account using SAS
   *  Attached svc by using SAS
      *  blob container, queue, table

* Interface also connects to data lake storage
* view/update entitiesin storage accounts

### Emulators
* Azure Storage Emu
  * local SQL Server 2012 express local db
  * emu table, queue, blob
* Azurite
  * node.js based
  * supports most azure storage commands through api

### Azure Data Lake Storage 
* Gen 1
* Gen 2

## Import/Export service
* secure
* large amounts of data to azure blob storage and azure files
* shipping disks to an azure data center
* data goes to 
  * blob storage
  * or azure files
* BitLocker usage to ship the disks in encrypted state and decrypt them
* WAImportExport tool
* Requires
  * requires the use of internal SATA II/III HDDs or SSDs
  * NTFS single volume per disk
  * Journal files for integrity
* Create jobs on 
  * azure portal
  * or Import/Export REST API
### Import
### Export


## AzCopy
* Supports azure Data lake storage Gen2 APis
* copy an entire account to another (blobs)
* acct to acct copy, using Put from URL APIs
  * quicker xfer
* List/Remove files and globs in given path
* wildcards, include, exclude
* resiliency
  * create job order/related log file
  * restart / resume jobs
  * auto retry on xfer

## Auth options
* Azure AD
  * azcopy login
  * Storage Blob Data Contributor role to write
* SAS tokens
  * append SAS token on blob path
  * supports Blob and File services