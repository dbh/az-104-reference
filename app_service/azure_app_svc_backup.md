- [azure app svc backup](#azure-app-svc-backup)
# azure app svc backup
* Tiers
  * Standard
  * Premium
*  App -> settings -> backups
*  restore app snapshot
   *  overwrite 
   *  or restore to another app
*  create app backups manually or on schedule
*  Backed up
   *  app config
   *  file content
   *  database connected to app
*  requires 
   *  azure storage account and container
*  note
   *  full backups are default
   *  partial supported
   *  can exclude files/folders from backup
   *  10 GB limit on zip
   *  firewall enabled storage account as dest for backup not supported