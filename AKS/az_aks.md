- [Azure Kubernetes Service](#azure-kubernetes-service)
  - [Scenarios](#scenarios)
  - [Terminology](#terminology)
  - [AKS Cluster and node arch](#aks-cluster-and-node-arch)
# Azure Kubernetes Service
* Container Orchestration system

## Scenarios
* scaling/orchestrating mult containers working together

## Terminology
* AKS - azure kubernetes services
* Pools - groups of nodes with ident configs
  * Nodes - VMs running containerized apps
    * pods - single instance of an app. Pod can contain mult containers
* Container - lightweight portable exec image. 
* Deployment - one+ ident pods , managed by Kubernetes
* Manifest - YAML file describing deployment

## AKS Cluster and node arch
* Azure-managed nodes
  * provide core Kubernetes services and orchestration
* Customer-managed nodes
  * where app workloads run
* upon creating AKS instance,  clusert node is auto created/config. 
* you pay for agent nodes (running)

* kubelet
  * kubernetes agent
  * processes orch requests from azure
  * schedules running of requested containers
* kube-proxy
  * handles virtual networking
  * proxy routes network traffic and manages IP addressing for svc and pods
* container runtime
  * component allows containerized apps to run and interact with addtl resources
    * virt net
    * storage
    * etc
  * runtime
    * AKS clusters
      *  Kubernetes 1.19+ node pools
         *  containerd
      *  Kubernetes < 1.19 node pools
         *  Moby (upstream docker)
* When creating AKS instance
  * init number of nodes
  * size
  * creates node pool
  * default node pool in AKS contains underlying VMs that run agent nodes