- [az container instances](#az-container-instances)
  - [General](#general)
  - [Azure Container instances](#azure-container-instances)
  - [Features](#features)
  - [Container groups ex](#container-groups-ex)
    - [Deployment Options](#deployment-options)
    - [Resource alloc](#resource-alloc)
    - [Networking](#networking)
    - [Common scenarios](#common-scenarios)
# az container instances

## General
* standardized and repeatable way to package, deploy, manage cloud apps
* don't need VMs and 
* without higher server tier

|feature|container|VM|
|-|-|-|
|isolation|lightweight from host and other containers. less secure boundary|complete iso from host os/other VMs|
|OS|run in user mode portion of os. Lightweight|complete OS on physical resources. more secure|
|deployment|deploy a container. docker cmd line. Orch via kube svc|VMs via Hyper-v, win admin center, PS in sys cnt virt machine mgr|
|persistent storage|azure disks for local storage single node, azure files for shared|use VHD for local storage single vm. SMB share for shared|
|fault tolerance|cluster node fail, containers recreated on good node|VM fail over to another server in cluster. VM's OS restart on new server|

## Azure Container instances
Fasted / simplest way to run container in azure

* port 80
  * container, web server, port 80
    * container host
      * virtual network

## Features
* fast startup times
* Public IP and DNS names
* Hypervisor level security
* custom sizes
  * nodes scaled dynamically to match actual resource demands
* persistent storage 
  * azure file share mounts
* lin and win containers
* coshceduled groups
  * scheduling multi-container groups, sharing host machine resources
* virt network deployment

## Container groups ex
* scheduled on single host machine
* assigned DNS name label
* exposes single pub IP, with one exposed port
* ex: 2 containers. 
  * one on 80
  * one on 1433
* includes azure file shares as volume mounts. each container mounts on share locally
* similar to kubernetes pod

### Deployment Options
common uses
* RM template or YAML file
* ARM template recommended, if need to deploy additional azure service resources
* YAML recommended if only container instances
### Resource alloc
* alloc resources like CPU, mem, GPUs to multi-container group
* adds resource requests of instances in the group
* 2 container instances, each requesting 1 CPU, you get 2 CPUs in container group
### Networking
* share external facing Ip
* share 1+ external ports on IP, and DNS label/FQDN
* container exposes port. that port exposed on FQDN. only one container in group can expose that port
### Common scenarios
* divide single f() task into smaller container images
* images delivered by diff teams, diff resource requirements
* ex
  * web app, pulling latest content from source control
  * app container and logging container
    * app -> logging svc/container -> logging to storage
  * app an dmonitoring containers
  * front-end and back-end
