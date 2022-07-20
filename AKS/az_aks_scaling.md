- [AZ AKS Scaling](#az-aks-scaling)
  - [General](#general)
  - [manually scale pods or nodes](#manually-scale-pods-or-nodes)
  - [Horizontal pod autoscaler (HPA)](#horizontal-pod-autoscaler-hpa)
    - [Cooldown of scaling events](#cooldown-of-scaling-events)
  - [Cluster autoscaler](#cluster-autoscaler)
    - [Scale out events](#scale-out-events)
    - [Scale in events](#scale-in-events)
  - [AKS Scaling to Azure Container Instances](#aks-scaling-to-azure-container-instances)
# AZ AKS Scaling

## General

* AKS
* may need to +/- amount of compute resources
* underlying number of nodes may need to change
* or mayneed to quickly provision lg # of additonal app instances etc

* AKS Cluster
  * Cluster Autoscaler
    * Node(s)
      * horizonal pod AutoScaler
        * Pod(s)

## manually scale pods or nodes
* can manually scale replicas (pods) and nodes to test how app responds w change in resources/state
* define set amount of resources to use fixed cost
* define replica or node count
* Kubernetes API schedules the rest

## Horizontal pod autoscaler (HPA)
* monitor resource demand
* auto scale replcias #
* checks Metrics API, every 30 sec
* works w AKS clsuters deployed w Metrics Server for K 1.8+
* config for given "deployment", 
  * define 
    * min, max replica #s. 
    * define metric to monitor


### Cooldown of scaling events
* prevent thrash after a change and race events
* how long HPA must wait before checking Metrics again
* down
  * 5 min
* up
  * 3 min

## Cluster autoscaler
* changing pod demands
* Cluster autoscaler changes number of nodes based on nodes in node pool
* checks every 10 sec
* Cluster AutoScaler works w RBAC enabled AKS. K 1.10.x or higher
* use alongside HPA
  * HPA +/- pods
  * CA +/- nodes


### Scale out events
* if CA notices pods cannot be scheduled b/c node pool constraint, # of nodes increases. Then pods can be scheduled to run on them
* If nodes not ready fast enough, pods may be in Wait state to be scheduled 
* Azure Container Instances - can scale an app w high burst demands. Virtual nodes


### Scale in events
* CA mon scheduling status for nodes
* if nodes didn't get requests for while, scale in. descrease node count
  * no longer needed for 10 min, boom
  * apps may exp disruption as pods scheduled on diff nodes when CA descreases # of nodes
    * avoid apps using single pod instance


## AKS Scaling to Azure Container Instances
* rapidly scale using integration w ACE
* K built in componetns to scale replicate and node count
* HPA may schedule too many pods for compute resources in node pool
  * if so, use Virtual Node config and Virtual Kubelet installed in AKS
    * ACIS acts as virt K node.
    * virtual nodes deployed to another subnet in same virt network
    * 
