# AZ Storage Access

* objects have URL
* storage account name is the subdomain of address
* //[storageAccountName].[storageType].core.windows.net
  * ex: //mystorageaccount.blob.core.windows.net/mycontainer/myblob

* custom domain
  * does not support HTTPS w custom domains
  * azure CDN access to blobs w custom DNS over https
  * CName record
    * blobs.contoso.com to contosoblobs.blob.core.windows.net
    * prepend "asverify." if domain already in azure. avoid downtime


## Secure endpoints
* must restrict network access to azure svcs 
* for Storage account use 
  * Firewalls and virtual networks
    * add virt network that will have access
    * can also allow pub ip ranges
    * must exist in same azure region or region pair of storage account


## Controlling access w shared access sigs (SAS)
* every request needs to be authenticated and authorized
* SAS
  * secure
  * delegated access to storage account
* Access azure storage
  * pub
    * StorageAccount
      * AllowBlobPublicAccess prop on storage account
    * Container level pub access
      * if anon access allowed on the storage account
  * AD
    * no need to stor creds in code
    * 2 step approach
      * Authen as sec principal
      * Oauth 2.0 token, then send token to AZ Storage to enable authorization on resource
  * Shared key
    * 2 512 bit access keys
    * share keys to grant clients access
    * root access to storage
    * use Azure Key Vault - key rotation on reg schedule etc
  * SAS
    * granular
    * sig types
      * user delegation
        * blob storage only
        * az ad creds
      * service sas
        * secured by storage account key
        * delegates access to resource in 1 of : 
          * blob, queue, table, file
      * account sas
        * sec with storage account key
        * same controls as service SAS
        * also access tos ervice level ops like Get Service Stats
    * can be assoc with stored access policy (upto to 5 SASs)

## SAS URI and Token
* URI
  * https://[storageAccount].[storageService].core.windows.net/[container]/[blobName.ext]?
* SAS Token
  |query param|Field name|desc|
  |-|-|-|
  |sp|signed perm|ops client can perf|
  |st|start time||
  |se|expiry time||
  |spr|signed protocol|ex https|
  |sv|signed version|service version of storage API|
  |sr|scope of resource|b (blob), c (container), d (dir), f(file), s (share)|
  |sig|signature|crypto sig|

## Creating SAS access in .NET
1. BobContainerClient
2. BlobClient
3. BlobSasBuilder object for blob to use
4. StorageSharedKeyCredential
   1. sasToken = ToSasQueryParams(storage shared key cred)

## Use stored access policies to delegate access to azure storage

* Anyone w correct SAS can access the file while valid
* revoke access keys 
* regeneration would require updating all apps using old shared key
* or...
  * SAS with Stored Access Policy

### Stored acced p9olicies
* Can be created on 
  * blob, file shares, queues, tables
* entry
  * Identifier
  * start time
  * expiry time
  * permissions
    * acdlrw

Process 
1. create stored access policy
   1. C#
   2. Portal
   3. CLI
2. create SAS tokens and assoc w stored access policies
   1. sas = BlobSasBuilder (on an identifier)
   2. sas.setPermissions(BlobSasPermissions.Read)
