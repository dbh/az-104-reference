# Azure RBAC
* crit f() for any org
* help mng access to resources, what can be done, areas of access
* authorization sys built on ARM
  * fine-graned access mgmt

## Concepts
* security principal
  * obj that is requesting access
  * ex: user, group, service principal, managed ident
* role definition
* scope
  * ex: Management group, sub, resource group, resource
* Assignment


## Implement

## What can it do?

## proc
### Create role def
* each role, defined in JSON
* ex: 
  * Actions
  * NotActions
  * DataActions
* built in
  * Owner
  * Contributor
  * Reader
  * ...
  * Backup operator
  * Security Reader
  * User Access Administrator
  * Virtual Machine Contributor
  * ... custom
    * ex: Reader support tickets
    * VM op

### Scope the role
* csv of ex
  * /sub/[sub id]
  * /sub/[sub id]/resourceGroups/[RG name]
  * /sub/[sub id]/resourceGroups/[RG name]/[resource]

### Create Role Assignment
* proc of scoping role def to a user, group, service principal, or managed ident


## Comparison AD vs Azure roles
|Azure RBAC roles|Azure AD Roles|
|-|-|
|mng access to azure resources|manage access to AD resources|
|scope to mult levels, mgmt group,sub,rg,r|Scope at tenant|
|role info accessed in az portal, cli, ps, ARM template, rest API|Role info in Az Ad portal, ms365 admin portal, Graph AzureAD, PS|

## RBAC to secure resources
* Grant partners and employees access
* grant access from 1 svc to another
* where people have access

* Role assignment
  * sec principal (who)
    * user,group,app
  * role def (what)
    * perms that can be performed
  * scope
    * access given at what level
    * mgmt group, sub, rg, resource