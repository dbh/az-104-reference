- [azure DNS Hosting](#azure-dns-hosting)
  - [Config Azure DNS](#config-azure-dns)
    - [Config private DNS Zone](#config-private-dns-zone)
    - [apex domain](#apex-domain)
    - [Alias records](#alias-records)
# azure DNS Hosting

* What is it
* How does it work
* DNS Server assignment
* DNS Lookups
* IPv4 and IPv6
* DNS Settings
* DNS Rec types
  * A
  * CNAME
  * MX
  * TXT
  * also
    * Wildcards
    * CAA
    * NS
    * SOA
    * SPF
    * SRV
* Record sets
* why
  * improved sec
  * easy
  * privte DNS domains
  * alias record sets
* security features
  * RBAC
  * Activity logs
  * Resource logs

## Config Azure DNS 
* create a zone
  * sub
  * RG
  * Name (domains name)
  * RG Loc
* Get the azure DNS servers
* updated domain registrar
* verify delegation of DNS
* config DNS settings
  * A
  * CNAME

### Config private DNS Zone
* Config
  * sub
  * RG
  * name
* ident vnets
* link vnets to private zone (private zone -> in virtual network links)

### apex domain
* @ symbol
* aka zone apex or root apex
* type
  * NS
  * SOA

### Alias records
* can point at 
  * traffic manager profile
  * azure CDN endpoint
  * pub IP
  * front door profile
* DNS supports
  * A
  * AAAA
  * CNAME
* reasons for alias records
  * prevent dangling DNS
    * couples lifecycle of DNS record with an azur resource
  * update DNS rec set automatically when IP addrs change
  * host LB apps at the zone apex
    * allow for zone apex resource routing to traffic manager
  * point zone apex to Azure CDN endpoints


See setup script 
[setup.sh](https://github.com/MicrosoftDocs/mslearn-host-domain-azure-dns/blob/master/setup.sh) for the example
