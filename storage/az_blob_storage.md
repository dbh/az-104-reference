# Azure Blob Storage

## Purpose
* large amounts of unstructured object data, such as text or binary data
* any type of unstructured data
* streaming video and audio
* data for back and restore, DR, archving
* store data for analysis

## Blob service resources
* Types
  * Storage account
  * Containers in storage account
  * blobs in container

* account
  * container
    * blob

* production
  * pictures container
    * img001.jpg blob
    * img002.jpg blob
  * movies container
    * mov1.avi blob

## Configure

### Create blob container
* all blobs must be in a container
* account can contain unlimited containers
* container can have unlimited blobs

* AZ Command
```bash
New-AzStorageContainer
```

* Azure portal
  * new container
    * set access level
      * private (no anon)
      * private (anon read access for blobs only)
      * container (anon read only for containers and blobs)

### Storage tier
|Tier|desc|
|-|-|
|hot|freq access. default|
|cool|lg amounts of data. less freq access. store >= 30 days. med expense on access|
|archive|2+ hour retrieval latency. Store >=180 days. low cost store. more expense to access|

### Rules for blob lifecycle
* ex, blobs lat modified more than _x_ days ago,
  * move to ____ storage 
  * delete the blob
* runs 1x a day to eval
* move aging data to cooler tiers
  

### Determine blob obj replication
* Scenarios
  * min latency
  * inc efficiency for compute workloads
  * optimize data distrib
  * optimizing costs
* object replication
  * async
  * copies blobs according to rules
  * configure 
    * src account
    * dst account  
  * src container -> dst
    * can be diff tiers
  * requires 
    * blob version enabled (both containers)
  * not supported
    * snapshots
    * archived

## Upload blobs
* any type
* any size
* types
  * block
    * spec block size on upload
  * page
    * up to 8 TB
    * frequent read/write ops
    * azure VM page blobs as OS and data disks
  * append
    * good for logging
    * based on block
* select type

### Tools
* AzCopy
  * easy to use
  * CLi
  * copy across containers or storage accounts
  * Built w Azure Storage Data Movement Lib
* Azure Storage Data movement lib (.net)
  * moving data between azure services
* Azure Data Factory
  * copy to/from
  * use acount key, shared access sig, svc principal or mg ident for azure resource auth
* Blobfuse
  * virt fs driver
  * use to access existing block blob data in storage account
  * linux fs
* Azure Data Box Disk
  * svc for xfer on-prem data to blob storage
  * helps w large datasets or network constraints
  * can request SSDs from MS
  * copy data to SSDs
  * Send back to MS for upload
* Azure Import / Export
  * svc for export lg amount of data from storage account to HD that you provide and then MS ships back with your data
* Azure Storage Explorer

## Pricing
### performance tiers
* Higher tier, more cost
* Cooler tiers, less cost
### data access costs
* increases as tier gets cooler
* charge per gigbyte for reads
### transaction costs
* per trans charge. Increases as tier get cooler
### Geo-Replicationdata xfer costs
* only applies when geo-replication configured (inc GRS and RA-GRS)
* per gig charge
### Outbound data xfer costs
* bandwidthused per gig
* consistent w/ general purpose storage accounts
### changing storage tier
* ex: change from cool to hot
  * incur read all data 
* ex: change from hot to cool
  * charge eq to write all data into cool tier (VPv2 accounts only)

## configure storage security
* Sec storage
  * generate shared access signature (SAS) tokens
  * manage access keys
  * configure azure AD Authenticaiton on storage acct

### Storage strategies
* encryption - auto encyrpted using Storage Service Encryption (SSE)
* Authenticaiton for Azure storage
  * Azure AD integration
    * data operations on Blob and Queue services
  * RBAC
    * roles scoped to storage account to security principals.
    * azure AD to authorize resource mgmt ops such as key mgmt
* data in transit
  * Client side encryption, HTTPS, or SMB 3.0
* disk encryption
  * Azure Disk encryption
* shared access signatures (SSE)
  * delegated access to data objects
  * granted using SAS

## Authorization options
* Azure AD
  * fine grained. user, group, apps RBAC
* Shared Key
  * account access keys and other params -> 
  * encryption sig string as Authorization header
* Shared Access Signatures  
  * delegate access to resource w account specified perms, over time interval
* Anon access to containers and blobs

### Create SAS
* URI granting access rights to resources
* Account and service level
* share w peeps who should not have access to storage account key
* Signing method
  * account key
  * user delegation key
* Perms
* Start, expire
* allows IPs
* Protocols
  * HTTP or HTTPS
* Generates
  * token
  * url


### URI and SAS params
|Name|Desc|
|-|-|
|Resource URI||
|Storage services version||
|services|blob or file service|
|resource types|svc level only|
|start time||
|expiry type||
|resource|sr=b  resource is a blob|
|permissions||
|ip range||
|protocol||
|signature|used to authenticate access to blob|

