- [Azure VMs - Connect](#azure-vms---connect)
# Azure VMs - Connect

* several ways
  * win
    * RDP
      * port 3389
      * Portal auto enables the connect button if VM is running, and reachable (pub/priv ok)
      * Get-AzRemoteDesktopFile
    * Windows Remote Management (WinRM)
      * port 5986 (can be changed)
      * command line session to azure VM
      * can also run non-interactive PS
      * can use certificates for additional session sec
      * cert goes in Key Vault
  * lin
    * SSH
      * scp
      * ssh
      * telnet
      * rlogin
      * raw socket
      * serial
    * authenticaiton
      * pw
      * pub/priv keys
        * azure requires >= 2048 bit key length SSH-RSA
  * Bastion
    * PaaS
    * provision inside virtual network
    * secure/seamless RDP/SSH connectivity to VMs
    * through Azure Portal
    * over ssl
    * public IPs not needed
    * 
