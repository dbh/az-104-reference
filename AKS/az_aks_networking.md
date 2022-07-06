- [az kubernetes networking](#az-kubernetes-networking)
  - [General](#general)
  - [Service types](#service-types)
  - [Pods](#pods)
# az kubernetes networking

## General 
* abstraction layer to virt networking
* nodes connected to to virt network
* aprovides inbound/outbound connectivity for pods
* kube-proxy run on each node to provide ^ network features

* Services logically group pods
  * all direct access via IP or FQDN on specific port
  * load balancer available
  * provide in/out connectivity for pods
  * Ingress controller for more complex routing
  * security and filtering network traffic possible with Kubernetes network policies

* Azure platform
  * simplify virt network for AKS clusters
  * on creation of K load balancer, underlying azure load balancer resource created and config
  * as opening network ports to pods, corresponding azure network security group rules configured
    * ex: HTTPS app routing, azure can also create external DNS as new ingress routes config

## Service types
* Cluster IP
  * internal IP for use in AKS cluster
    * internal only apps which support workloads in cluster
* Node Port
  * create port mapping on underlying node
  * allows app to be accessed with node ip and port
* Load Balancer
  * creates azure load bal resource
  * configure ext ip
  * connects requested pods to load bal backed pool
  * IP of LB can be dyn or static
    * external and internal static IP can be assigned
    * static ip often tied to DNS
  * allow cust traffice to reach app
    * load bal rules created on desired ports  
  * Internal and External LBs avail
* External Name
  * creates specific DNS entry for easier app access



## Pods
* K uses pods to run instance of app
* pod ~ single instance of app
* typical 1:1 w container
* advanced scenarios
  * pod w multiple containers
    * mult-container pods scheduled on same   node
* when creating, define resource limits 
  * (cpu/mem)
  * max resource limits
* pods usually deployed/managed by K controllers, like Deployment controller