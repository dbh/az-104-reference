- [Az Incident Response](#az-incident-response)
  - [General](#general)
  - [Signal types](#signal-types)
  - [Composition of an alert rule](#composition-of-an-alert-rule)
  - [Activity log alerts](#activity-log-alerts)
  - [Create svc health alert](#create-svc-health-alert)
  - [Smart groups](#smart-groups)
# Az Incident Response

## General
* robust alerting and mon in azure monitor
  * config notifications and alerts, key sys and apps


## Signal types
* metric
  * threadshold exceeded etc
* activity log
  * azure resource changes states
* log
  * app returned 404

## Composition of an alert rule
* resource
* condition
* actions
* alert details
  * 0 crit
  * 1 error
  * 2 warning
  * 3 info
  * 4 verbose

## Activity log alerts
* types
  * Specific ops
  * Service health events

* composition
  * category
  * scope
  * rg
  * resource type
  * op name
  * level (verbox .. critical)
  * status 
    *  Started, failed, succeeded
 *  event init by

* resource specific log alert
  * ex: filter on"Activity Log - Administrative" to filter options
  * activity log (signal type)
  * select type of alert (ex: VM powered off)

## Create svc health alert
* diff
* Service health -> Health alerts -> create service health alert
* actions
  * email, sms, create azure app push notification, voice call, f(), trigger logic app, create itsm ticket, webhook, runbook
* can reuse activity groups (like operations email distrib list)

## Smart groups 
* reduce noise
* name ~ taxonomy
* machine learning algs
* Azure monitor joins alerts based on repeat occurance or sim
* smart group states
  * new
  * acknowledged
  * closed