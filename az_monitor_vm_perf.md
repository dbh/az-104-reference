- [Az Monitor Vm Perf](#az-monitor-vm-perf)
  - [Tools](#tools)
    - [Azure Monitor Logs](#azure-monitor-logs)
    - [Log Analytics workspaces](#log-analytics-workspaces)
    - [Azure Monitor VM Insights](#azure-monitor-vm-insights)
  - [other](#other)
  - [Plan log analytics workspace deployment](#plan-log-analytics-workspace-deployment)
    - [Strategy](#strategy)
    - [Data collect compute/monitoring data using agents](#data-collect-computemonitoring-data-using-agents)
# Az Monitor Vm Perf

## Tools
### Azure Monitor Logs
* collect and org log data from azure resources
* store in log analytics workspace
### Log Analytics workspaces
* query for analysis, reporting, alerting
* win event logs, heartbeat, perf data, syslogs
* container
* diff levels of access

|access mode|desc|notes|
|-|-|-|
|access mode|how users access workspace. define data scope|workspace context or resource context|
|access control mode|def how perms work for any Log Anal. ws|1. require ws perms, 2. use resource or workspace perms (RBAC)|
|table level RBAC|granular data control inside Log Anal. ws|allow admin define specific data types access to users. Cust roles to gran/deny for specific tables. w/ either workspace context or ersource context access models config|
### Azure Monitor VM Insights
* relies on Azure Monitor Logs
* predefined, curated monitoring exp, 
* little config
* "InsightMetrics"
* admin can query perf/usage

## other
* Azure Monitor Metrics
  * % cpu usage, etc
  * stored in time-series
  * near real-time reporting/alerting


## Plan log analytics workspace deployment
* pick right design
* containers where azure monitor data is collected, aggregated, analyzed
* diff types of logs can be ingested

### Strategy
* limit total # workspaces for daily ops
* makes admin and query exp easier/quicker
* maybe mult workspaces if global company, sep workspaces for data sovereignty

### Data collect compute/monitoring data using agents
|Agent|Desc|Notes|
|-----|----|-----|
|azur emonitor agent|coll from gues OS on VMs. deliver to Monitor logs/metrics|event replace log analytics agent and azure diag ext. understand tradeoffs|
|log analytics agent|coll logs and perf from VMs in azure, clouds, or on-prem|allow onboard azure monitor VM insights, VM defender for cloud, MS Sentinel. work a azure automationa ccounts / Azur eupdate management, azure automation state config, azure automation change tracking and inventory|
|azure diag ext|cust receive extra data from guest OS and workloads on compute resources|data mostly sent to Az Monitor Metrics. also Event Hubs to go 3rd party, Azure storage for archival. boot diag|
|dep agent|certain processes on VMs|maps all deps between VMs and external process deps|

