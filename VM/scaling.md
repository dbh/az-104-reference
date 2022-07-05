- [Vertical and Horizontal scaling](#vertical-and-horizontal-scaling)
  - [Types](#types)
    - [vertical](#vertical)
    - [horizontal](#horizontal)
  - [Considerations](#considerations)
  
# Vertical and Horizontal scaling

## Types
### vertical
* +/- VM size
* svc built on VM is under-utlized, -> reduce VM size to reduce monthly cost
* inc VM size to cope with larger demand w/o creating new Vms
* more limitations
  * max VMs per region
  * availability of larger hw
  * require stop/restart

### horizontal
* scale out
* add more VMs to handle load

## Considerations
* reprovisioning - removing an existing VM and replacing it with a new one. Need to retain data?