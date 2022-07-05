# azure_deploy_w_arm_template

* JSON ARM Template
* VS Code
* deploy project's infra . declarative and reusable. 
* versioned
* came before Bicep

## Commands
* az login
* finding commands
  * az find secret
  * az network nsg --help

|resource type|cli command group|
|--|--|
|RG|az group|
|VM|az vm|
|storage accounts|az storage account|
|key vault|az keyvault|
|web apps|az webapp|
|sql db| az sql server|
|cosmos db|az cosmosdb|

### Global args
* --help
* --output
  * json (default)
  * jsonc
  * tsv
  * table
  * yaml
* --query
  * JMESPath query lang
* --verbose
* --debug

## Interactive mode
* az interactive

## What is infra as code
* consistent config
* improved scalability
* faster deployments
* better traceability

## ARM template
* idempotent
* can be broken into smaller templates
* can be used in pipelines
* 