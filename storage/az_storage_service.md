# Storage Service 

## Storage Service Encryption
* Data at rest
* auto
* disks, blob, queue, table, files
* AES 256
* Use key vault or Key Vault's API

### enc type
* MS Managed keys
* Cust Managed keys
  * more flex and control
 
## Best practices
* always req HTTPS to distrib/create SAS
* Ref stored access policies where possible
* near-term expiration times on an unplanned SAS
* req client auto renew SAS if necessary
* Care around SAS start time
  * at least 15 min in past or not set at all
* be specific w resource to be access
  * min required privs
  * access to min amount. single entity ex. 
  * read only etc
* Remem billing for usage, incl w SAS
* Validate data writtenusing SAS
* use storage analytics to mon app