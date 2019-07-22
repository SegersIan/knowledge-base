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
  
* Availability Zones
  * VMs are in different physical locations within a Region. (cross Zone)
  * 99.99% SLA
  * 2 Categories
    * **Zonal Services** : Add a resource to a specific zone (VMs, Disks, Ips...)
    * **Zone-redundant services** : Atu replication accross zones (e.g. for SQL DB)
  * Don't support all VM sizes.
  * **Protect from enitre data center failure (so a zone that goes down)**
  
* An Availability zone in an Azure region is a combination of a fault domain and an update domain.
  * Meaning, the fault domain and update domains are 100% isolated between zones. You can't have 2 VMs in different zones being on a same fault and/or update domain.

* Disaster recovery approaches: 
  * Sync replication of apps and data using : **Availability Zones**
  * Async replication of apps and data using : **Region Pairs**
    * Cross region

* Azure Management services are resilient from region-level failures.

## Storage

* Managed Disks