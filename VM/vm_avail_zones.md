- [VM Availability Zones](#vm-availability-zones)
  - [Impl](#impl)
# VM Availability Zones
* high avail offering
* protect from data center failures
* zones are within a region
* each zone 
  * 1+ data centers
* min of 3 zones in a region
* zone redundant svcs replictae apps/data across zones to protect from single points
* With Availability Zones, Azure offers industry best 99.99% VM uptime SLA.

## Impl
* zonal services
  * pin resource to zone
  * vm, disk, standard ip
* zone-redundant services
  * platform auto replicates across zones
    * zone-redundant storage, sql database etc