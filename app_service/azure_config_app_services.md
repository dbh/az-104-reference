- [azure config app services](#azure-config-app-services)
  - [Scenarios](#scenarios)
  - [Skills](#skills)
  - [Langs](#langs)
  - [Reasons](#reasons)
  - [Create an app](#create-an-app)
# azure config app services

## Scenarios
* new website for business
* running existing web app on aging on-prem server

## Skills
* create app svc
* secure it
* configure custom domains
* configure backup for app svc
* configure network settings
* configure deployment settings
* monitor and backup
* config app insights

## Langs
* .net
* node.js
* php
* java
* python (on linux)
* html
* Custom windows/Linux container

## Reasons
* mult langs and frameworks
* devops
* global scale and high avail
* connections to SaaS and on-prem data
* sec and compliance
* app templates
* VS integ
* API and mobile features
* serverless code

## Create an app

* Details
  * name
  * pub 
    * code
    * docker container
  * runtime stack
    * 
  * os
    * linux / windows
  * region
* app settings
  * always on
    * even when no traffic
    * req for webjobs or webjobs triggered usin gcron
  * ARR affinity
    * multi-instance deployment, sticky sessions
  * connection strings
    * encrypted at rest
    * transmitted over encrypted channel