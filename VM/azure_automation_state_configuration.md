- [Azure Automation State Configuration](#azure-automation-state-configuration)
  - [prob](#prob)
  - [What](#what)
  - [Target](#target)
  - [PowerShell DSC](#powershell-dsc)
  - [LCM - local Configuration manager](#lcm---local-configuration-manager)
  - [Push and pull architectures in DSC](#push-and-pull-architectures-in-dsc)
    - [Comparison](#comparison)
  - [Platforms](#platforms)
  - [DSC Req for win](#dsc-req-for-win)
  - [Use of Powershell DSC](#use-of-powershell-dsc)
  - [Pull config for nodes](#pull-config-for-nodes)

# Azure Automation State Configuration

## prob
* Mult identical VMs deployed
* should stay configured same way
* config of each Vm could shift

## What
* Built in PowerShell DSC
* consistently deploy, monitor, automate update state of all resources. Apply to VMs
* create desired state config script
* keeps VMs in cluster in same state
  
## Target
* on or off prem
* Win or Linux

## PowerShell DSC
* declarative management platform for AASC
  * configure, deploy, control systems
* scripts should be idempotent

* config
  * imports
  * Node
    * resource block
      * details


## LCM - local Configuration manager
* component of Windows Management Framework (WMF) 
* responsible for updating state of a node, like a VM to match cesired state
* LCM run
  * get state of node
  * test/compare
  * set to match/update
* configure LCM when register a VM with azure automation


## Push and pull architectures in DSC
* LCM on a node
  * Push mode
    * admin manually sends or pushes configs to one or more nodes
  * pull mode
    * pull server holds config info
    * LCM on each node polls from pull server
      * 15 min
      * get latest config details

### Comparison
* Push mode easy to setup
* pull mode useful in enterprise deployment
  * lg # machines
  * regularly polls pull server and updates nodes w desired state

## Platforms
* Win
  * server 2019, 2016, 2012, 2012 R2 SP1
  * 11, 10, 8.1.7
* Linux
  * DSC Extension

## DSC Req for win
* Azure DSC VM Extension uses WMF
* WinRM - windows Remote Management
  * Win server 2012 or later, win 7 or later
* proxy avail
* Windows Server 2008 R1 SP1, win 7, or later
* other
  * port TCP 443 for outbound
  * global url: *.azure-automation.net
  * Agent service URL (uses workspaceId)


## Use of Powershell DSC
* Declarative scripting lang
* focus on outcome, not journey

```ps1
Get-DscResource | select Name,Module,Properties
```


Resources
* File
* archive
* environment
* log
* package
* registry
* script
* service
* user
* windowsfeature
* windowsOptionalFeature
* windowsProcess

```
Configuration configName {
    Node "localhost" {
        WindowFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'Web-Server'
        }
    }
}

```

* Can take params
```
param
(
    [string] $ComputerName='localhost'
)
```

* multiple node blocks

```
Node @('WEBSERVER1', 'WEBSERVER2', 'WEBSERVER3')
```

* resources (one or more blocks)
* Config block compiles into Managed Object Format (MOF) doc
* config data in DSC script
  * config block
  * scoped to named nodes or all nodes
  * AllNodes

```ps1
$datablock =
@{
    AllNodes =
    @(
        @{
            NodeName = "WEBSERVER1"
            SiteName = "WEBSERVER1-Site"
        },
        @{
            NodeName = "WEBSERVER2"
            SiteName = "WEBSERVER2-Site"
        }
    );
}
```

* secure credentials in DSC
* PSCredential object
* pass PSCredential into DSC script
* creds not encrypted by default in .mof
  * use cert in config data
  * certs config through node's LCm
  * PS 5.1, .mof files on node are encrypted at rest. in transit, encrypted by WinRM

Push config to a node
```ps1
Start-DscConfiguration -path D:\
```

## Pull config for nodes
* config Azure Automation account to act as pulls vc
* upload config to Automation account
* register VMs w account
* in automation account 
  * import any PowerShell modules needed by DSC

* on each VM
  * install DSC VM Extension
  * install WMF
  * LCM applies desired state
