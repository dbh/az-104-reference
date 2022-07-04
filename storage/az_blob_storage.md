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