- [azure app service plans](#azure-app-service-plans)
  - [App Svc Plan Details](#app-svc-plan-details)
  - [how run / scale](#how-run--scale)
  - [Considerations](#considerations)
  - [Determine app svc plan pricing](#determine-app-svc-plan-pricing)
    - [Free](#free)
    - [shared](#shared)
    - [Basic](#basic)
    - [Standard](#standard)
    - [Premium](#premium)
    - [Isolated](#isolated)
  - [Scale up and out app svc](#scale-up-and-out-app-svc)
  - [Config app svc plan scaling](#config-app-svc-plan-scaling)
    - [Considerations](#considerations-1)
# azure app service plans

* web app scaling for 
  * high demand
  * saving money by reducing resources on less demand

## App Svc Plan Details
* region
* number of VM instances
* size of VM Instances
  * small, medium, large

## how run / scale
* tier
  * free/shared
    * app receives CPU minutes on shared VM
    * cannot scale out
  * other
    * app is in an app service plan
    * all vminstances configured in app svc plan
    * if mult apps in same app svc plan, all run on same VMs
    * diagnostic logs, backups, webjobs use same CPU cycles / memory on same VMs
  * app svc plan
    * scale unit of App Service Apps
    * ex   
      * 1
        * 5 VM instances
        * all apps run on all five instances
        * if autoscale configured
          * all apps in plan scaled out together based on autoscale settings


## Considerations
* Save money putting mult apps in one app svc plan
* apps in same plan all share same compute resources
* determine if necessary reources?
  * understand capacity of app svc plan and expected load for new app
  * overloading can cause downtime for new/existing apps
* isolate into sep plan
  * app is resource intensive
  * want to indep scale 
  * app needs resources in diff geo region

## Determine app svc plan pricing
Tiers
### Free 
* dev/test
* 10 apps
* 1 GB
* no auto scale
### shared
* dev/test
* 100 apps
* 1 GB space
* no auto scale
### Basic
* dedicated dev/test
* unlim apps
* 10 GB space
* no auto scale
* max instances up to 3
### Standard
* prod workloads, ehance scale and perf
* unlim apps
* 250 GB space
* autoscale 
* 20 deployment slots
* max instances up to 30
### Premium
* high perf, sec, isolation
* unlim apps
* 1 TB space
* autoscale 
* 20 deployment slots
* max instances up to 100
* upgrades
  * Prem plan, Prem v2, features
    * Dv2 series Vms, SSD, double mem to core ratio from std
    * higher scale 
### Isolated
* mission critical
* run in virt network
* private, dedicated env in azure datacenter
* Dv2 series VMs
* "App Service Environment"

## Scale up and out app svc
Choose
* manual scale
  * maintain fixed instance count
* custom autoscale
  * schedule based on any metrics
* scale up
  * get more CPU, mem, disk, extra features like dedictaed VMs, custom domains, certs, staging slots, autoscaling
  * change pricing tier on app service plan
  * change tier at any time
* scale out
  * Inc number of vm instance for app
  * as man as 30 instances dep on pricing tier
  * App Svc Env in Isolated tier further inc scale-out to 100

## Config app svc plan scaling
* autoscale settings
* scale mode
  * metric or to specific instance count
* rules
  * metric
    * CPU usage > 50%, response time, # requests etc
  * time
* instance limits
  * min
  * max
  * default
* schedule

### Considerations
* rules
  * have matching/corresponding rules for scale in and scale out
* config notifications