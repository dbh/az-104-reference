- [Az App Gateway](#az-app-gateway)
  - [General](#general)
  - [Other features](#other-features)
  - [Determine App Gateway Routing](#determine-app-gateway-routing)
    - [Path-based routing](#path-based-routing)
    - [Multiple site routing](#multiple-site-routing)
    - [other](#other)
  - [App gateway component setup](#app-gateway-component-setup)
  - [web app firewall (WAF)](#web-app-firewall-waf)
  - [Health Probes](#health-probes)
# Az App Gateway

## General

* manage requests that client apps send to web app
* app layer routing routes traffic to pool of web servers, based on URL

* browser -> app gateway -> HTTP/HTTPS listener -> Rule (Http Setting) -> Pool -> something in pool
* backend pool
  * Vms
  * VM scale sets
  * app svc
  * on-prem servers... 
* Algorithm -> Round Robin
* App gateway provides stickiness within session

## Other features
* proto: HTTP(S), HTTP/2, websocket
* web app firewall 
* end-to-end request enc
* autoscaling

## Determine App Gateway Routing
* 2 methods 
### Path-based routing
* diff URL patterns to diff pools
### Multiple site routing
* more than 1 web app on same app gateway
* register mult DNS names (CNAMEs) for Ip addr of gateway, w each site name
* app gateway uses sep listeners for each site
* each listener passes request to diff rule
* multi-tenant apps. each tenant has own set of VMs or resources for hosting web app

### other
* redirection
* Rewrite on HTTP headers
* Custom error pages

## App gateway component setup
* mult components that combine to route requests to pool of web servers and check health
* components
  * Front end
    * listener
      * port
      * cert
      * rule
        * Http Setting (port, stickiness, probe, timeout)
          * Custom Probe
        * Back end pool
* FE IP
* App GW can have FE IP
  * Public 0-1
  * private 0-1
  * both
* listeners
  * 1+
  * basic listener type - route only on URL
  * multi-site listener: all route based on host in URL
  * handle TLS/SSL certs
* routing rules
  * bind listener to back end pools
  * assoc set of http settings
  * whether/how traffic is enc between app gw and back-end servers
  * proto, session stick, conn draining, timeout, health, etc
* back-end pools
  * coll of web servers
  * spec IP of each web server and port, when config pool
  * pool can be set # of VMs, VM scale set, app in app services, or coll of on-prem servers

## web app firewall (WAF)
* optional
* handle incoming requests
* based on OWASP
* common threats:
  * SQL injection, cross-site scripting, command injection, HTTP Request smuggling, remote file inc, bots, crawlers, canners, HTTP proto violations, and anomolies
* OWASP defined set of generic rules
* Core Rule Set (CRS)
  * CRS 2.2.9
  * CRS 3.0 (more recent)

## Health Probes
* app gateway sends health probe
* status code 200-399 is healthy
* if unconfigured, default created, probe every 30 sec