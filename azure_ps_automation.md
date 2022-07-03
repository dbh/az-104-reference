# azure powershell automation

## benefits
* optimize workflow for administration
* common, repeated tasks

## Tools available
* azure portal
* azure cli
  * available: 
    * inside Azure cloud shell (in browser), or 
    * local instal on lin/mac/win=
* azure powershell
  * az ps - add module to powershell
  * connects to azure sub and manage resources
  * available
    * in Azure cloud shell
    * local installin/mac/win
  * modes
    * interactive
    * scripted

### Install powershell and extension
* Base powershell product (avail on win, mac, lin)
* azure az powershell module 

### PS commandlets
* interactive or
* cmdlet: scripted / commandlets
* verb-noun naming convention
* Single action
* Get-Help -Name Get-ChilItem -Detailed
* Get-Module to download/install a new module (DLL)
* Update-Module


### PS Flow
* import az cmdlets
* connect to az sub
  * Connect-AzAccount
* create rg
* verify

### CmdLets
* Get-AzContext
* Set-AzContext (subscription)
* Get-AzResourceGroup
* New-AzResourceGroup -Name xx -Location yy
* Get-AzResource
* New-AzVm
  * Set-AzVMOperatingSystem
  * Set-AzVMSourceImage
  * Add-AzVMNetworkInterface
  * Set-AzVMOSDisk
* Common verbs
  * Remove
  * Start
  * Stop
  * Restart
  * Update
  * Get
  * Set 
  * New

## Create and save PS Scripts
* PowerShell ISE
