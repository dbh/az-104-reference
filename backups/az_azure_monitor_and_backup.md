- [Az Azure Monitor And Backup](#az-azure-monitor-and-backup)
  - [Data Collector API](#data-collector-api)
  - [activity log events](#activity-log-events)
    - [Query the log](#query-the-log)
# Az Azure Monitor And Backup

* enables gathering monitoring and diag info about health of services
* viz/analyze prob that might occur in app
* query logs
* alert/action on log events

* azure monitor
  * collect metrics and logs from a bunch of things
  * capture
  * send/show/process/view
    * inisghts
    * viz
    * analyze
    * respond
    * integrate

* define
  * metrics
    * lightweight
    * near real-time 
    * some aspect of a system at point in time
    * Metric Explorer
  * logs
    * rec with diff sets of props for each. events and traces. perf data, etc
    * Data Explorer
    * stored in Log Analytics w rich query lang

* data types
  * app monitoring data
  * guest OS mon data
  * azure resource mon data
  * azure sub mon data
  * azure tenant mon data

## Data Collector API
* collecte and monitor anything with a rest API

## activity log events
* 90 day retention
* subscription level events in azure
* data from azure resource manager, service health events, all kinds of stuff
* write events
  * who , what , when for write ops on REST resources
* logs help determine
  * what ops taken on resources 
  * who started the op
  * when it occured
  * status of op
  * values of other props to help
  
  ### Query the log
  * filter it 
    * sub
    * time
    * severity
    * RG
    * Resource
    * Resource type
    * op name
    * by whom
    * search
* categories
  * admin
  * service health
  * resource health
  * alert
  * autoscale
  * recommendation
  * security
  * policy
  * 