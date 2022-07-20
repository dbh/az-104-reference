- [azure vm extensions](#azure-vm-extensions)
  - [General](#general)
  - [Custom Script Extensions (CSE)](#custom-script-extensions-cse)
  - [Desired State Config (in PS)](#desired-state-config-in-ps)
    - [configuration](#configuration)
    - [DSC](#dsc)
# azure vm extensions

## General
* automate task of creating, maintaining, removing VMs
* extension does this
  * small apps  
  * post-deployment config
  * automation tasks on VMs
* ex:
  * install softare
    * anti-virus prot
    * config script inside VM
* ext can be
  * managed by CLI, powershell, ARM templates, azure portal
  * bundled with new VM deployment or run against existing sys
* Diff extensions for diff OS


## Custom Script Extensions (CSE)
* auto launch /exec VM customization ask post config
* ex
  * stop VM
  * install software
  * or series of tasks
* install CSE from azure portal, VMs, Extensions
* Create and Provide powershell script
  * arguments you want to pass in
* after upload, immediate exec
* scripts can be downloaded from AZ Storage or Github or provided at extension runtime in portal

Powershell

Requires URL for blob container of PS file
```bash
Set-AzVmCustomScriptExtension
```

consider
* timeout
  * 90 min
* deps
  * make sure deps are available
* failure events
  * will script stop if there is an error, like out of disk space or security restriction?
* sensitive data
  * may need creds etc. how to protect?


## Desired State Config (in PS)
* deploying/managing config data for sw services and manage env
* set of Windows PS lang extensionss, cmdlets, resources
* declarative 
* centers around creating configurations
### configuration
* script
* env made up of computres (nodes) w specific characteristics
* char ex: 
  * Specific windows feature is enabled
  * deploying sharepoint
* Use DSC when CSE won't work for app

### DSC
* Configuration block
* node block (s, 1+)
* resource block(s, 1+)

