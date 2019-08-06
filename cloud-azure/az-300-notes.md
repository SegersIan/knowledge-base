# AZ-300 Study Notes

## Various

* Global filter for subscription and (active) directory
* Every single resource specifies a region to be stored
* Azure hides more the concepts of zone's (as in HA Zone)
* Zone's are more explicit in "availability sets"
* Resource Groups are mandatory


## Zones, Regions and High Availability

Primary [Source](https://docs.microsoft.com/en-us/azure/availability-zones/az-overview)

* Business Continuity is the business word for HA and Recovery.
* A zone can be one ore **more** data centers still.
* Each region has **a min of 3** zones.

* Availability Sets
  * A group with 2+ VMs in the same Data Center.
  * Parameters
    * Fault Domain : Each fault domain has own hardware network switch and power source. 
    * Update Domains : All VMs in same update domain restart together during planned maintenance.
  * So the Fault Domain is a hardware logical grouping, while the update domain is a software logical grouping.
  * Can't add existing VMs to an availability set
  * This is all within one 
  * 99.95% SLA
  * **Protect from hardware failures and maintenance within data centers**
  * Usually a set per tier
  * When you create a VM you can assign it to an Availability Set Resource
  
* Availability Zones
  * VMs are in different physical locations within a Region. (cross Zone)
  * 99.99% SLA
  * 2 Categories
    * **Zonal Services** : Add a resource to a specific zone (VMs, Disks, Ips...)
    * **Zone-redundant services** : Atu replication accross zones (e.g. for SQL DB)
  * Don't support all VM sizes.
  * **Protect from enitre data center failure (so a zone that goes down)**
  * When you create a VM you can assign it to an Availability Zone number
  
* An Availability zone in an Azure region is a combination of a fault domain and an update domain.
  * Meaning, the fault domain and update domains are 100% isolated between zones. You can't have 2 VMs in different zones being on a same fault and/or update domain.

* Disaster recovery approaches: 
  * Sync replication of apps and data using : **Availability Zones**
  * Async replication of apps and data using : **Region Pairs**
    * Cross region

* Azure Management services are resilient from region-level failures.

## Networking

* Virtual Network (aka VNet)

* Subnet
  * Can be designated/delegated to be used by a dedicated Azure Service (Like workspaces/volumes/...)

* A VM connects through a NIC which is assigned to the VM and connected to a subnet
* Azure provides implicitly a Internet Gateway, you don't need to provision one like in AWS.

* [Outbound connections for VMs](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-outbound-connections)

* [Virtual Network Service Endpoints](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview) : Extend private address space and identity over a direct connection to Azure services.
  * Allow a direct network connection to your other Azure resources/services without leaving Azure backbone network.
  * Not available to all Azure services, but some examples : Storage, DB's, Key Vault, Event relates services and App service.
  * More secure than to have VM call a Azure service and hopping over the public internet
  * Optimal Routing because of not making the internet hop
  * Less IP management (like NAT's etc)
  * Azure service resources secured to Vnets are NOT reachable from on-premise. Because everything goes through Azure backbone network, so no public IPs as there is not internet hop.
    * To allow this,  **allow public IPs** or use **ExpressRoute**
  * Can be connected to a specific subnet (so only the App tier can access service x)
  
* Better to define a username/password for a vm in a private tier, else the jump box needs to be configured with a *.pem file for `ssh`

* Network Security Group has stateless rules.

* [Network Security Group vs. Application Security Group](https://www.kainos.com/microsoft-azure-nsgs-asgs-simplified/)
  * **(NSG) Network Security Group** is the Azure Resource that you will use to enforce and control the network traffic with
    * Applied to a subnet **or** a virtual machine
    * Has default rules
  * **(ASG) Application Security Group** is an object reference within a Network Security Group.
    * Used within a Network Security Group
    * Apply a rule to specific workload or group of VMs
    * Such a rule has a "network object" and a explicit IP address
    * Seems that they are statefull, like the Security Group in AWS
    * No default rules
    * No rule order
    * Examples
      * Allow internet traffic (source internet) to destination Web tier (DMZ-ASG), ports 80 and 443
      * Allow DMZ traffic (source DMZ-ASG) to destination App tier (APP-ASG), ports xxx
      * ...
      
* For a LB, you define independently a "Health Probe" which you can then refer to in a routing rule or other.

## Virtual Machines

* System assigned managed identity : Like assigning a role in AWS, so a VM can access services without auth in code.
* `Cloud init` : Script that runs when it boots **the first time**.
* You cannot put a VM in a Vnet which is located in another region.

* A VM can change it's size after having been created
* You can give a VM a public IP and then only allow SSH access if you don't want to use a jump box.
* When putting VM's in a backend pool of a LB, and you want to SSH into it, create an Inbound NAT rule + double check inbound NSG.

* TODO : Multiple data disks, why ? (maybe one OS disk and one attached for temporary data storage, so when does that clear ? After reboot ?)

