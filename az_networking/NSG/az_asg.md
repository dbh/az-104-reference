- [Azure Application Security Group](#azure-application-security-group)
  - [what](#what)
  - [Limits](#limits)
# Azure Application Security Group

## what
* enable config network security as extension of app structure
* group Vms and define network sec policies based on groups
* reuse sec policies 
* w/o worhing about explicit IPs

## Limits
* max ASGs per sub.
* in a single rule
  * at most ASG as source and 1 ASG as dst
* ASGs can only have NICs in the same VNEt
* ASGs (src and dst) must bein same virt network