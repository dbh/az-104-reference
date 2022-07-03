## Azure Resource Manager

* Infra for app has many components
* work w app's resource as a group
* deploy/update/del all resources for solution as a whole
* use template for deployment
* ARM
  * sec
  * audit
  * tagging
* Provides
  * Consistent managerment layer
  * via
    * PS, CLI, portal, REST API, client SDKs
  * ARM talks w Authentication
  * all requests go through ARM to appropriate resource providers
* Serve diff environments
* declarative templates 
* define deps and orders
* tagging for org

## Terminology
* resource
* resource group
* resource provider
  * ex: Microsoft.Compute
  * Microsoft.Storage
  * Microsoft.Web
* template
  * in JSON
* declarative syntax

## Notes
* each resource provider has set of operations and resources for azure service
* naming convention
  * provider/type
  * ex: Microsoft.Keyvault/vaults


## Locks
* levels
  * sub
  * rg
  * resource
* inherited by lower levels
* types
  * RO
  * delete 

## Reorg azur resources

## xxx

## ARM Templates
# 256 param limit
# JSON
# Required elements
* Schema
* Version
* Resources



## Bicep templates
* DSL
* Declarative syntax (again_)
* less verbose than JSON
* Type-safe
* abstraction over ARM template JSON

* Bicep template -> Resource Manager -> auto conversion to JSON ARM template -> azure
* simple syntax
* string interp instead of concat, or functions
* modules
* auto dep mgmt
* type validation and intellisense

