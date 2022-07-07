- [VM Manage by CLI](#vm-manage-by-cli)
  - [Tools](#tools)
  - [Creation](#creation)
  - [Sizing](#sizing)
  - [Listing the VMs](#listing-the-vms)
  - [Show details](#show-details)
  - [Query / filter with JMESPath](#query--filter-with-jmespath)
  - [Start](#start)
  - [Restart](#restart)
  - [Instance view](#instance-view)
  - [Install sw on the vm](#install-sw-on-the-vm)
# VM Manage by CLI

## Tools
* Command line tools
  * CLI (bash)
  * PowerShell
* asl same tools via Azure Cloud Shell
* Write scripts

az vm ....
* create
* deallocate
* delete
* list
* open-port
* restart
* show
* start
* stop
* update

https://docs.microsoft.com/en-us/cli/azure/reference-index

* params
  * --resource-group
  * --name
  * --image
  * --location
  * --verbose

## Creation

* on creation
  * auto creation of private and public ip

  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.237.147.119",

  ssh azureuser@<public-ip-address>

  az vm image list --output table

  az vm image list --publisher Microsoft --output table --all

  az vm image list --location eastus --output table

## Sizing

```bash
az vm list-sizes --location eastus --output table
```

|type|Desc|sizes|
|-|-|-|
|General purpose|balanced CPU/mem. dev/test|Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7|
|Compute optimized|High CPU to mem ratio. med traffic app, network app, batch|Fs,F|
|Mem opt|High mem to CPU, rel db, med to lg cache, in-memory analytics|Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D|
|storage opt|high disk io. big data, sql, nosql|Ls|
|GPU Opt|VMs targeted for heavy graphics|NV,NC|
|High perf|most powerful CPU VMs, optional high throughput network RDMA|H,A8-11|


resize
```bash
az vm list-vm-resize-options \
    --resource-group learn-03e62768-d6bc-4a81-9591-6c0f9bb642e9 \
    --name SampleVM \
    --output table

az vm resize \
    --resource-group learn-03e62768-d6bc-4a81-9591-6c0f9bb642e9 \
    --name SampleVM \
    --size Standard_D2s_v3

```

## Listing the VMs
 az vm list --output table

 ```bash
 az vm list-ip-addresses -n SampleVM2 -o table
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM2         20.228.65.191        10.0.0.4
```

## Show details
```bash
az vm show --resource-group learn-03e62768-d6bc-4a81-9591-6c0f9bb642e9  --name SampleVM2
```

## Query / filter with JMESPath

ex: Get the SKU for the VM image
```bash
 az vm show --resource-group learn-03e62768-d6bc-4a81-9591-6c0f9bb642e9  --name SampleVM2  --query storageProfile.imageReference.sku
 ```

 "18.04-LTS"

 ```bash
 az vm show --resource-group learn-03e62768-d6bc-4a81-9591-6c0f9bb642e9  --name SampleVM2   \
 --query "networkProfile.networkInterfaces[].id" -o tsv
 ```

## Start
```bash
az vm stop \
    --name SampleVM
    --resource-group ...
```
## Restart


## Instance view

```bash
az vm get-instance-view --resource-group learn-6aced856-43a8-481c-9384-82410cb43df3 --name SampleVM2  --query "instanceView.statuses[?starts_with(code,'PowerState/')].displayStatus" -o tsv
```

VM running


## Install sw on the vm

steps 
1. get IP of VM
2. ssh azureuser@pub_ip
3. sudo apt-get -y update && sudo apt-get -y install nginx
4. exit
5. open the port
```bash
az vm open-port \
    --port 80 \
    --resource-group learn-6aced856-43a8-481c-9384-82410cb43df3 \
    --name SampleVM2
```
6. curl it on the public ip