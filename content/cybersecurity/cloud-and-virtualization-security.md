# Cloud and Virtualization Security

## Exploring the Cloud

* **oversubscription** - allocates more virtual resources than physical resources actually available, betting that not all customers will use their full allocation simultaneously.
* **multitenancy** - Different users share resources in the same cloud infrastructure.

### Benefits of the Cloud
* On-demand self-service computing
* Scalability (vertical & horizontal) - rapidly increasing capacity
* Elasticity - expand and contract capacity as needed
* Measure Service - You pay for waht you consume
* Agility & Flexibility

### Cloud Roles

* **Cloud Service Providers** - offer the cloud computing
* **Cloud Consumers** - ones that consume the cloud computing
* **Cloud Partners/brokers** - Resell supplementary products or services in regards of the cloud
* **Cloud Auditors** - independents that audit cloud services and operations
* **Cloud Carriers** - The network service provider that delivers connectivity between cloud consumers and providers.

Anyone can take multiple roles, like neptune was a Cloud consumer and service provider.

### Cloud Service Models (XaaS)

* **IaaS** - Customer does full config
* **PaaS** - Run apps that customer developed themselves, but without granualr network/infrastructure responbilities
  * Example **FaaS** upload just the code and it will execute on an event without further overhead.
* **SaaS** - Customer only does config in the "application", see ERP, CRM, ..
* **Managed Service Providers (MSPs)** - service organizations that are responsible for all tech infrastructure for a customer.
  * If they offer security, they are **Managed Security Service Providers (MSSPs)**

### Cloud Deployment Models

* **Public Cloud** - Default - Shared infrastructure for the general public/anyone
* **Private Cloud** - provisioned for a single customer
  * Build/deployed by either a 3th party or the organization itself.
  * More excess resources, so less cost efficient
* **Community Cloud** - Like Public multitenant, but all tenants are from the same community that share same needs or mission (e.g. regualrity needs, compliance, etc..)
* **Hybrid Cloud** - catch all of blending public, private and/or community
  * Requires technology to unify the different clouds into single coherent platform

Note: The intelligence community uses "Private Public" cloud. The infrastructure resides in a CIA facility, but provides (for example) decicated AWS services. Azure Arc allows to use Azure platform but on hardware/infrastructure you manage yourself. So it is a private cloud, but it uses the functinality/platform layer from a public cloud.

* **Public Cloud bursting**- You use only public cloud to expand capacity when necessary, but by default use private/on-prem

### Shared Responsibility Model
Your security responsibilities fall in the "customer responsibilites", the vendor area secuirty is for, the vendo
![ing](../assets/cloud_responsibility_matrix.jpg)

### Cloud Standards and Guidelines

![img](../assets/cloud_reference_architecture.png)

* [NIST Cloud Computing Reference Architecture](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication500-292.pdf)
  * This shared understanding helps to also talk about cybersecurity.
* **Cloud Security Alliance (CSA)** - industry organization focused on best practices in cloud security.
    * [CSA Site](https://exams.cloudsecurityalliance.org/en)
    * Designed the [Cloud Controls Matrix (CCM)](https://cloudsecurityalliance.org/research/cloud-controls-matrix) to help understand the right use of cloud security controls and map those to various regulatory standards.
* **Edge Computing** - Push some of the (pre-)processing to the edge/sensors before shipping it back to the central server/cloud.
* **Fog Computing** - Local gateway devices close to the sensors that does the preprocessing before sending it to the central server/cloud.

## Virtualization
Is made possible by hypervisors, virtual machines don't know they're in a virtual environment.

### Hypervisors

* Hypervisior is a special OS that mediates access to underlying hardware resources.
* Primary responsibility : Enforce vertical isolation between the VMs.
  * Gives the VM the illusion that its a single independent physical device.
  * VM's are not able to access/information/resources assigned to another VM.
* Types
  * **Type I Hypervisor AKA Bare-metal hypervisor** - Operate directly on underlying hardware
    * Most efficient and default for datacenter virtualization
    * THIS IS the OS
  * **Type II Hypervisors** - Run as an application on top of an OS (e.g. Parrallels, VirtualBox)
    * THIS IS AN APP installed on another OS
    * More for personal computers, hobby, but less efficient.

## Cloud Infrastructure Components
### Cloud Compute Resources
* **Virtual Machines** - OS level virtualization
  * Specify assigned hardware, OS, pay on consumption, SSH/RDP for access.
* **Containers** - Application level virtualization
  * Same security concerns as VMs, isolation of access and resources

### Cloud Storage Resources
* **Block Storage** - for VMS
  * Preallocated, so you pay for that.
  * Most expensive
* **Object Storage** - S3
  * You pay for how much actually used
  * Cheaper
* **Security Considerations**
  * *Set permissions Properly*
  * *Consider high availability and durability*
  * *Use encryption to protect sensitive data*

### Cloud Networking

* **Software defined networking (SDN)**
* **Software defined visibility (SDV)** offer insights into the traffix of the virtual networks
* **Security Groups** -
  * kind of the Firewall feature
  * work at network and transport layer
  * WAF works on higher levels (application layer for example)
  * Usually no cost
* **Virtual Private Cloud (VPC/VNET)**
  * Segmentation - Different security levels on differenet subnets.
    * Similar grouped systems can talk to each other, others not.
    * On hardware level they would use VLAN (Virtual LAN) instead of virtual subnets.
  * VPC endpoints - CSP backbone that allows to connect VPC with each other
  * Cloud transit gateways is to connect a VPC with your on-prem network directly and securily
    * Requires physical actions and efforts.

## Cloud Security Issues
### Availability
* Baselevel services don't always provide High Availability, you need to configure/architect accordingly.
### Data Sovereignty
* Data is subject to legal restrictions of any jurisdiction where it is collected, stored or processed.
* you might be subject to laws that you don't have much to do with, just cause your data is hosted there.
* Encrypt data, to keep control of your data, even when it goes over different jurisdictions, but understand what your situation is.
### Virtualization Security
* **Virtual Machine Escape Vulnerabilities** - most serious, it breaks the isolation between VMs in data and/or resource access.
* **Virtual Machine Sprawl** - When user creates IaaS VM and forgets about it and it accrues cost and security issues
* **Resource Reuse** When hardware resources assigned to one customer is reassigned to another, and there was no proper cleanup, like old data still there.
### Application Security
* See [Application Security](application-security)
* **API Injection Technology** - inspect API requests for security issues (e.g. WAF)
* **Secure Web Gateways (SGWs)** - monitors egress web requests and evaluates agains security policies.
  * in other words, an egress firewall/WAF
  * mostly work on application layer
  * Some do Network and transport layer
### Governance and Auditing of Third-Party Vendors
Auditiability of a CSP is important.

## Hardening Cloud Infrastructure
* Cloud native controls
  * Have direct integrations and are more cost effective
* 3th party solutions
  * more costly, but integrate with various CSPs
* or combined

### Cloud Access Security Brokers (CASBs)
Software tools that serve as intemediaries between cloud service users and cloud service providers.
This allows for monitoring user activity and enforce policy requirements, 2 different approaches:

* **Inline CASB solutions** - physically/logically reside in connectio path between the user and service.
  * Requires configurtion of network and/or endpoints.
  * Allows to see and block requests before they arrive at cloud service.
* **API-Based CASB solutions** - Interacts directly with CSP's API
  * No real changes/reconfigurtion to be done
  * Unable to block requests
  * More limited to monitoring and reporting
  * Fixs policy violations after the fact.

### Resource Policies
Policies to limit actions or users can make. (eg. you can only deploy in region x)

### Secrets Management
Offer **Hardware Security Modules (HSM)** for internal key usage but also for customers. Keys are generated and never exposed externally.
