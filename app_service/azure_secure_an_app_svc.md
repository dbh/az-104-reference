- [Azure - secure an app svc](#azure---secure-an-app-svc)
  - [built-in authentication and authorization](#built-in-authentication-and-authorization)
  - [Basics](#basics)
# Azure - secure an app svc

## built-in authentication and authorization
* azure web apps support auth*
  * sec
  * federation
  * encryption
  * JSOn
  * JWT mgmt
  * grant types... 
  * blah blah
  * 

## Basics
* identity provider
  * authenticates users w specified provider
  * validate, store, refresh tokens
  * manage authenticated session
  * injects ident info into request headers
* configuration settings
  * allow annon requests
  * allow only authenticated requests
    * /.auth/login/<provider>
* logging and tracing
  * log files
  * the trace logs, look for references to a module named EasyAuthModule_32/64.