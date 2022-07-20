- [Azure App Service - Host an app](#azure-app-service---host-an-app)
  - [What](#what)
  - [Need](#need)
  - [Deploy](#deploy)
    - [Audo deploy](#audo-deploy)
    - [manual](#manual)
# Azure App Service - Host an app

## What
* full managed
* web app hosting platform
* PaaS
* build app while azure takes care of infra, scaling,e tc
* deployment slots
* CI/CD
  * Azure DevOps
  * GitHub
  * Bitbucket
  * ftp
  * local Git repo
  * once connected, azure takes care of build and deploy
* Deployment Center
* Visual Studio publishing and FTP publishing
* Built-in auto scale

## Need
* sub
* rg
* app name
* publish (how)
  * code, docker image, etc
* runtime spec
* OS
* Region
* app service plan
  * set of virt server resources
  * plan has a size/sku/pricing tier
  * can have mult apps

## Deploy
### Audo deploy
* Azure DevOps
* GitHub
* Bitbucket
* OneDrive
* Dropbox
### manual
* Git
* az webapp up
* zip deploy
* war deploy
* vs 
* FTP/S
