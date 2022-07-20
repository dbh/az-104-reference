- [Azure VPN Gateway high availability](#azure-vpn-gateway-high-availability)
  - [Active/standby](#activestandby)
- [Active/Active](#activeactive)
# Azure VPN Gateway high availability

## Active/standby
* every azure vpn gateway has 2 instances in an active-standby config
* for maint or disruption
  * standby instance takes over automatically
  * resumes S2S VPN or Vnet to VNet connections
  * swith over w brief interruption
* planned main
  * connectiivty restored 10-15 seconds
* unplanned
  * depends
    * about 1 min to 1.5 min for worst case
    * P2S VPN client connections to gateway and P2S Connections disconnected and users will have to reconnect

# Active/Active
* both Azure VPN Gateway instances active
  * each has unique pub IP
  * each established con to on-prems VPN dev
* 2 on-prem VPNs active
  * configure to accept 2 connections or make to 2 connections to the 2 Azur eVPN Gateway IPs
