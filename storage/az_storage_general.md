# AZ Storage
## General

Implement
* Durable and highly available
* secure
* scalable
* managed 
* accessible
  * http,https
  * sdks
    * .net
    * java
    * node.js
    * python
    * php
    * ruby
    * go
    * rEST APi
  * CLI, PowerShell, portal
* storage for
  * VMs
  * unstructured data
  * structured data
    * Tables, cosmos db, azure sql db, etc
* tiers
  * standard
  * premium
* cannot convert 1 tier to the other

## Services
### Containers (blob)
* Massible scalable object store
  * text
  * binary
* servce image/docs directly to browser
* distrib access for files
* streaming
* backup
* data for analysis
### Files
* managed file shares, cloud, on-prem, hybrid
* config files for mult VMs could be on a common share
* tools/utils used by mult developers etc
* diagnostic logs, metrics, crash dumps can be written here
* Storage account credentials used to provide authentication for file share access. Anyone with mounted share full read/write access
### Queues
* messaging store, reliable msg between app components
* store/retrieve messages
* up to 64 KB per msg
* contains millions messages for async processing
### Tables
* nosql store for schemaless storage
* now part of Cosmos DB
* Azure cosmos DB Table API

## Determine storage account kind
* standard general purpose v2
  * blob, file, queue, table, data lake storage
* premium block blobs
  * high trans rates
  * smaller objects, consistently low storage latency
* premium file shares
  * enterprise or high perf file share apps
* premium page blobs
  * high-perf page blob scenarios

## replication options
* Local Redundant storage
  * reundancy in same data center only
  * cheapest, default option
  * use if 
    * data easily reconstructed
    * data constantly changing, storing data not really required
    * app restricted to replicating data only within country due to data gov
* Zone Redundant Storage
  * redundant across data centers
  * synchronous
  * 3 storage clusters in single region
  * not available for all regions
  * changing to ZRS from something else, req data movement (stamps)
* Geo-Redundant Storage
  * redundant across regions
  * 2nd region, hundreds of miles away
  * 16 9's durability
  * GRS/RA-GRS
    * 1st rep to LRS
    * on update, commit to primary loc using LRS
    * replicate sync to 2nd region using GRS
      * within _nd region, rep to LRS
  * GRS is avaiable and read only if MS initiates swap over to 2nd region
  * RA-GRS is avaiable RO, even if no problem exists
* Geo-Zone Redundant Storage
  * protection from regional outages (like Geo Redundant)
  * Protection from Zone outages
  * rep across 3 azure avail zones in primary region
  * replicated to 2nd geo region from regional disasters
  * regions paired w another in same geo, "geo pair"
  * Continue to Read/Write even if avail zone unavailable
  * 16 9's
  * MS Recommends for 
    * consistency
    * durability
    * high avail
    * perf
    * resilience