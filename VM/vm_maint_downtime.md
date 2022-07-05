- [VM Maintenance and Downtime](#vm-maintenance-and-downtime)
# VM Maintenance and Downtime

Planned and Unplanned failures
3 scenarios
* Unplanned hw maint
  * azure predices hw or any platform component is about to fail
  * Live Migration tech to migrate VMs
    * pauses VM for short time
* unexpected downtime
  * hw or phys infra for VM fails unexpectedly
  * local network, disk, or rack level fails
  * azure platform auto-heals/migrates VM in same data center
  * VMs expereience reboot
* planned maint
  * periodic updates
  * most without impact