- [Azure DNS](#azure-dns)
  - [General](#general)
  - [Configure](#configure)
  - [Verify](#verify)
  - [Azure Zones](#azure-zones)
    - [delegate](#delegate)
    - [child domains](#child-domains)
    - [record sets](#record-sets)
  - [Private DNS zones](#private-dns-zones)
    - [determine priv zone scenarios](#determine-priv-zone-scenarios)
      - [name res for mult networks](#name-res-for-mult-networks)
# Azure DNS

## General
* host/config/admin DNS for org on az infra
* same creds,APIs, tools, billing
* on creating a sub, initial domain name created [subname].onmicrosoft.com
* custon domain
  * point the initial domain name / sub ofer to a custom domain name
* req: Global Admin
* custom domain name must be added to "your directory" and verified

## Configure

## Verify
* on initial add, custom domain name is unverfied
* 1 directory - 1 domain name
* verification by adding DNS record
  * MX
  * TXT
* azure will query DNS name for presence of record. min to hours
* on verify complete, DN added to sub

## Azure Zones
* azure DNS 
  * reliable/secure DNS service to manage / resolve DN in virt network
  * DNS Zone hosts DNS records for domain
  * each DNS record for domain goes in DNS zone
  * azure portal - add DNS zone
    * num records
    * rg
    * loc sub
    * name services

### delegate
* need to know name servers in done
* Azure DNS allocs name servers from a phone, when zone created
* azure DNS auto created authoritative NS recs in zone
* go to registrar's entry for domain
  * change DNS servers over to the ones from azure

### child domains
* create delegate subdomain 
* same as delegation, except NS records must be created in parent zone in az, ratehr than in registrar
* can be in same or diff RGs

### record sets
* diff between "sets" and individual entries/records
* set = collection of records in zone, having same name and are same type

## Private DNS zones
* throughout and within virt networks
* good for oganization
* zones can be config w
  * "split-horizon" view - priv and pub DNS zone sharing same name, resolving to diff answers

### determine priv zone scenarios

#### name res for mult networks
* vnet1 as Registration virt network
* Vnet2 Resolution virt network
* share common zone contoso.lab
* Resolution and Registration virt networks linked to Zone
* DNS records for Registration network auto created
* manually add DNS rec for Vms in Resolution virt network
* Reverse DNS also works within the same virt network