# Azure Svcs via CLI

* automation
* Re-run scripts, consistency
* std deployment commands
* always same parameters


## Install
* Can be installed on Linux, MacOS, win
* similar to bash
  
## Capabilities
* control almost every aspect of every resource
* work w rg, storage, VMs, AD, containers, ML, ... 
* commands grouped
  * groups subgroups
  * ex:
    * storage (group)
      * account (sub-group...)
      * blob
      * queue
* az find blob
* az find "az vm"
* az storage blob --help

## Proc to create a resource
* az login
* az group create --name X --location y
* az group list
* az group list --output table
