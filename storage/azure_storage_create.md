# AZ Storage Accounts
* container that groups AZ Storage svcs together
* only data services in AZ Storage can be included in storage acct
* need one storage acct per different set of settings you want.

## Account settings
* name
* deployment model
  * Resource manager, Azure Resource Manager API
    * newer
    * recommended
    * supports concept of Resource Groups
  * Classic (Azure service management API)
* account kind
  * StorageV2 (general purpose v2)
    * current offering. all storage types and features
  * Storage (general purpose V1)
    * legacy. all storage types but not all features
  * blob storage
    * legacy. only block blobs and append blobs

## Account creation tool
* Az portal
* CLI
* PS
* Management client libs

Scripting with CLI or PS recommended if automation needed. 

az portal other wise, b/c storage accounts not frequently created


# AZ Storage
* Blob
* File
* Queues
* Tables

## Factors
* department for billing
* locality to ____/ office / .... 
* data diversity
  * country
  * region
  * private or public
* cost sensitivity
* critical vs non-critical
* each acct addes management overhead/complexity

ex
* azure sub
  * rg1
    * storage account
  * rg2
    * storage account
    * storact account

Other data svcs, not storage. indep resources
* Azure SQL
* Azure Cosmos DB

Storage account settings
* Sub
* Location
* Perf
  * std. 
    * any data service. 
    * uses magnetic disk drives
  * premium
    * more svcs.
    * block blobs
    * append blobs
    * specialized file storage for premium file shares
    * SSD
* replication
  * min: 
    * 3 copies of data in same data center, assoc with storage account
    * Locally Redundant Storage (LRS)
  * extra $
    * Geo-reundant Storage (GRS)
* access tier
* Sec Transfer required
* Virt networks