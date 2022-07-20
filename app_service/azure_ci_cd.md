- [azure CI CD](#azure-ci-cd)
  - [CI/CD Features](#cicd-features)
  - [Manual deployment](#manual-deployment)
  - [Deployment slots](#deployment-slots)
    - [Add deployment slots](#add-deployment-slots)
      - [Swapped](#swapped)
      - [Not swapped](#not-swapped)
# azure CI CD

## CI/CD Features
* DevOps, GitHub, Bitbucket, FTP, local git repo on dev machine
* app service does the rest
  * auto sync code
  * future changes on code
* define own build and release process 
  * compile, run tests, build, release, deploy

## Manual deployment
* Git
  * use Git URL
  * pushing to remote repo will deploy app
* CLI
  * webapp up from cli
  * package it up and deploy it
* VS
  * App Service deployment wizard
* FTP/S

## Deployment slots
* Tiers: Standard, Premium, Isolated
  * can use dedicated slots instead of prod slot
  * live apps with own hostnames
  * app contant and elements can be swapped between two slots, inc prod
* advantages
  * validate changes in staging deployment slot before swapping w prod slot
  * deploying app to slot first and swapping it to prod ensures all instances of slot are warmed up
  * eliminate downtime on deploy
  * seamless traffic redirection
  * swap back if needed

### Add deployment slots
* new can be empty or cloned
* config editable on clone
* some elements are not slot specific and some are. what does this mean?
  * slot specific app settings, connections trings, if applicable
  * continuous deployment settings, if enabled
  * app service authentication settings, if enabled

#### Swapped
* general, such as framework, ver, web sockets
* app settings (can be made sticky)
* conn strings (can be made sticky)
* handler mapping 
* pub certs
* webjobs content
* hybrid conns *
* service endpoints *
* azure CDN *


#### Not swapped
* publishing endpoints
* custom domain names
* non-pub certs
* tsl/ssl settings
* webjob schedules
* ip restrictions
* always on
* diagnostic settings
* CORS
* virt network integration
