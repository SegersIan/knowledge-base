# Security Governance and Compliance

## Security Governance
* **Governance programs** - Set of procedures/controls put in place to allow an orgization to effectively direct its work.

### Corporate Governance
> Ensure that organizations set an appropiate direction, develops a plan to implement that direction and then execture its plan.

In public companies, there are too many and volatile "owners" (shareholders), impossible for them to vote on every important thing, therefore corporate governance models exist.

* **Typical Corporate Governance Model**
  * *Shareholders* elect a `board of directors`
  * *Board of directors* appoints and manages a `CEO`
    * Typically drawn from the major shareholders.
    * Majority of directors should be *independent directors*, having no significant relationship with the organization aside of their as board member. Reason being, employees can be assigned a board member position, but that might cause conflict of interest.
    * Meet monthly/querterly, so no daily operations
  * *CEO* appoints and managers the `management team`.
    * Managers daily operations.
* *Note* This is a typical model for public owned companies, private and non profit can have very different models. It is what it says it is "Typical".
* **Internal Commities** of subject matter experts (SME) may be incorperated.
* **Government/Regulatary agnencies** might also play role in governance of an organization (e.g. with Banks)

### Governance, Risk, and Compliance (GRC) Programs
* **GRC Programs integrate**
  * 1. Governance of the organization
  * 2. Risk maangement
  * 3. Compliance"

### Information Security Governance
* **Natural extension to corporate governance**
* **Chief Information Security Officer** the top guy about infromation security usually.
  * *Does not have operational control* of the origanization, so must collaborate with all other senior management.
  * It's not a rogue function, no unilateral decisions, you must respect and following reporting lines.
* **Policies** help to implement (Cybersecurity Requirements) across the organization
  * Remember, the CISO has no operational control, so this is a tool to get things done in the entire organization.

### Types of Governance Structures
* **Centralized Governance Models** (Top Down)
  * Central authority creates `policies` and `standards`
  * Central authorirt enforces throughout the organization.
* **Decentralized Governance Models** (Bottoms Up)
  * Business units are delegated `objectives`
  * each Business unit implements as they see fit.

## Understanding Policy Documents
* **Information Security Policy Framework** contains documents that are designed to describe the cybersecurity progam of an organization.
* Generally include **4 types of documents**: Policies, Standards, Procuedures and Guidelines
  * These categories vary from organization to organization, as long they achieve their desired purpose.
* **What influences your policies**
  * *Organization's business objectives*
  * *Regulatory and legal requirements* (e.g PCI-DSS)
  * *Industry-specific considerations* (e.g. Banking)
  * *Jurisdiction-specfifc considerations* (e.g A land, state, village...)

### Policies
* **Short: High-Level statements of management intent.**
* **Compliance with a Policy is mandatory**
* **Approval** is high level (e.g. CEO). By keeping the policies very high level, the CISO remains flexibility to adapt and change specific requirements,
  * So a policy will refer more to `there will be standards` and not `those 5 specific standards`
* **Content** - Broad statements about cybersecurity objectives
  * Examples
    * Statement about importance of Cybersecurity to the organization.
    * Requirement that anyone + contracts takes measures to protect CIA properties
    * Designation of CISO or other lead/executivie on cybersecurity
    * Delegation of authorit to CISO or whatever executive on cybersecurity
  * Avoid details and concrete things
    * Else it needs re-appoval and high maintance of the document. Cause changes happen regularly
* **Examples** of Policy documents
  * *Information Security Policy* - High level authorirt and guidance about securiry program.
  * *Incident Response Policy* - how will respond to security incidents
  * *Acceptable Use Policy (AUP)* - clear direction on permisslbe use of information resourcs
  * *Business Continuity and Disaster Recovery Policy* ensure essential business functions continue to operate during and after disaster and that data/assets are recovered/protected.
  * *Software Development Life cycle (SDLC) Policy* How the SDLC incorperates Cybersecurity
  * *Change Management and Change Control Policies* How changes are controled, reviewd, implemented, ...

### Standards
* **Short: Requirements describing how an organization will execute policies**
* **Compliance with a Standards is mandatory**
* **Approval** At lower organization level, therefore, change more regularly
* **Content**
  * May be specific configuration settings used for a common OS
  * Controls that must be in place for highly sensitive information
  * Other securty objectives...
* **Examples** of Standards documents
  * [University Of Berkeley - Minimum Security Standards For Electroniic Information](https://security.berkeley.edu/minimum-security-standards-electronic-information)
    * Defines information in 4 Data Protection LEvels and what controls are required for each level.
  * *Password Standards* password requirements, reuse, length,....
  * *Access Control Standards* account lifecycle (from provision, active-use, to deprovision).
    * Should clarify difference (or lack off) between users and contractors.
    * Dictates needs of passwords for sytems, devices, ...
  * *Physcial Security Standards* Access COntrol Systems, Cameras, security personel, visitor access, handloing of breaces.
  * *Encryption Standards*

### Procedures
* **Short: Detailed, step-by-step processes for specific circumstances**
* **Compliance with a Procedures is mandatory**
* **Approval** At lower organization level, therefore, change more regularly
* **Content**
  * Ensure a consisten process of achieving a security objective.
* **Examples** of Procedures documents
  * How to build a new system
  * How to release code to production
  * How to respond to security incidents
  * [VISA - What to do do if compromised](https://usa.visa.com/dam/VCOM/download/merchants/cisp-what-to-do-if-compromised.pdf)
  * *Change Management procedures* - how change is being done
  * *Onboarding and offboarding procedures* - of employees/guest/contractors
  * *Playbooks* - Actions for incident response team

### Guidelines
* **Short: Best practices and recommendations to a given concept/tech/task**
* **Compliance with Guidelines is optional**
  * Can be open for discussion in some culture, so it CAN happen.
* **Approval** At lower organization level, therefore, change more regularly
* **Content**
  * Ensure a consisten process of achieving a security objective.
* **Examples** of Procedures documents
  * How to build a new system
  * How to release code to production
  * How to respond to security incidents
  * [VISA - What to do do if compromised](https://usa.visa.com/dam/VCOM/download/merchants/cisp-what-to-do-if-compromised.pdf)
  * *Change Management procedures* - how change is being done
  * *Onboarding and offboarding procedures* - of employees/guest/contractors
  * *Playbooks* - Actions for incident response team

### Exceptions and Compensating Controls
> Provide a mechanism for exception to rules (polices, standards, and procedures).

* The *Policy framework* should provide on the `requirements` to qualify for exemption and `who` can approve the exemption.
* Exceptions can require **Compensating Controls** to mitigate the associated risk.
* If there are compensating controls *temporarily*, there should be *remediation* plan to go to the orignal designated plan.

### Monitoring and Revision
* **Evaluate implementation and efficacy of Policies on regular basis**
* **Security Information and Event Management (SIEM)** systems help with that.
  * Also conducting period audits/assesments.
  * Also how wel policies are being adhered to.
  * Also how wel policies still make sense (changes in tech, goals, ...)
  * Also review feedback from staff
* **Revisions** happen based on the monitoring and learnings/conclusions out of them.
  * Must be communciated to all relevant personal + training.

## Change Management
> Ensure that systems maintain the same level of securtity.
> Change management helps **reduce unanticipated outages** caused by unauthorized changes.
> Related to the A in CIA.

* **Balance** between usability and security often, sometimes security is lowered ot achieve a reasonable usability.
* **Audit** allows in forensic and other situatiuons to audit, analyse and understand what changes happend in the lead up of an security event.

### Change Management Processes and Controls
* **A change management process allows for securit impact analysis**
  * What will be the security impact of this change?
* **Standard Operating Procedures For Changes**
  * 1. *Request the change*
  * 2. *Review the change*
    * Might be an indiviual or a Change Advisory Board (CAB)
  * 3. *Approve/Reject the change*
    * Record/document the decision.
  * 4. *Test the change*
    * Results to be added to change documentation
  * 5. *Schedule and implement the change.*
    * *Backout plan* in case unforeseen problems happen.
  * 6. *Document the change*
* **Also in emergencies, this should be followed**

### Version Control
* **Developers/Users have access to latest versions**
* **Changes are carefully managed**
* **Labeling/numbering system**

### Documentation
> Identifies the current configuration of systems and who is responsible and its purpose.
> Lists all changes done since the baseline config.

## Personnel Management
> An employee has access to systems and info.
> This access is a risk that intentional/accidental actions cause a cybersecurity incident.

Following best pratices help reduce employee-centered risks.

### Least Privilege
> A person should be granted only the minimum set of permissions necessary to carry out their job function.

* Not easy
* Permission creep
* Required permissions might change regulary

### Separation of Duties
> When a job function is extremely sensitive, the function can be split/seperated so 2 different people are required to complete that said job function.
>
> Example: Finance, one can request a pay out, another must do/approve the payout.

* **Two-Person Control** similar to Seperation of duties, except :
  * Seperation Of Duties takes 2 people with different privileges
  * Two-Person control requires participation of 2 people to perform a single sensitive action.

### Job Rotation and Mandatory Vacations
* **Job Rotation** - Rotate employees with sensitive role periodically to other positions in the organization with different privileges.
  * Reason: Much fraud requires ongoing concealment.
* **Mandatory Vacations** - By revoking people their access during a mandatry vacation, you can  stop more ongoing effors of concealment.

### Clean Desk Space
* **Clean Desk Policies** to product confidential or sensitive information by limiting paper exposed on employee their desks. All papers/materials must be secure before leaving your desk.

### Onboarding and Offboarding
* **Standeraized processes for onboarding and offboarding**
* **Background checks** to risk assess the new hire.

### Nondisclosure Agreements (NDA)
> Require employees, contractors or vendors to protect any confidential information

### Social Media
> Constraint behavior of employees on social media based on how positively/negatively it might reflect upon the organization.

## Third-Party Risk Management
> Many risks come from 3th party organizatiions with whom you do business.
> Vendors, Partnerships, ...

### Vendor Selection
* **Due Diligence** vet your potential vendors
  * Vendor's financial stability, reputatiom, quality of productsservices and compliance with relevant regulations
  * Vendor's security and data handling practtices
* **Conflict Of Interest** - competing interest of the vendor that might influence their behavior that is not in your own interest.
  * Can be mitigated with contractual clause or not picking the vendor.

### Vendor Assessment
> Even after initial selection, ongoing due diligence and conflict of interest analysis should find place.
* **Penetration Testing** helps asses this.
* **Right-To-Audit Clause** allows to do an audit and request audit results
* **Independent Assesments** Like ISO27001 and SOC reports.
* **Supply Chain Analysis** understanding the vendor's supply chain
* **Questionairs** to the vendor to collect information on various things, like data handling, security, etc...

### Vendor Agreements
* **Master Service Agreements (MSA)** umbrella contract for the work that a vendors does with an organization over time.
  * Security & Privacy Requirements
  * Then indivdual projects can get a Work Order (OW) and refer to the MSA for "reusable" agreements
* **Service Level Agreements (SLA)** Written contracts to specify the conditions of a service provided by the vendor.
  * If vendor fails to meet SLA, consuquences are laid out.
  * Examples: availability, durability, response time, ...
* **Memorandum Of Understanding (MOU)** (informal) document aspects of the relationship, often internally.
  * Examples: A platform team internally supports other teams
  * Documents the relationship and avoid future misunderstandings
* **Memorandum Of Agreement (MOA)** (formal) document agreements and terms between parties, mutual understanding of roles and responsibilities in fulfulling specific objecgives.
  * More details than MOIs
* **Business Partners Agreements (BPA)** when 2 companies do business as partners.
  * Content: Responsbilities, division of profit...
  * Example: Jointly develop a product

### Vendor Monitoring
* **Goal**: Manage and mitigate 3th party Risk.
* **Includes** Continious observation and alaysis of vendor performance and compliance.
* **Rules Of Engagement** Boundries withinthe vendor should operate in.
  * Clear communication protocols, responsibilities, processes and issue resolution.
  * Sets both parties on same page on expecations and obligations to avoid disputes and misunderstandings.
* **Performance Monitoring** set KPIs to measure vendors performance.

### Winding Down Vendor Relationships
> Take steps to have an orderly transition when a vendor relationship ends or a product/service is discontued from the vendor.

## Complying with Laws and Regulations
### Common Compliance Requirements
* **Health Insurance Portability and Accountability Act (HIPAA)** - US
  * Security & privacy for health care providers, insures and information clearinghouses in US.
* **Payment Card Industry Data Security Standard (PCI DSS)** - International
  * Storage, processing and transmission of credit/debit card info.
* **Gramm-Leach-Bliley Act (GBLA)** - US
  * Security program required an a responsible person
  * Financial Institutions
* **Sarbanes-Oxlet Act (SOX)** US
  * Storage and Processing
  * Financial records of Publicly traded companies
* **General Data Protection Regulation (GDPR)** - International
  * Primairly Privacy and a bit security
  * Is a worldwide regulation for ANYONE processing data about EU residents.
* **Family Educational Rights and Privact Act (FERPA)** US
  * Privacy and Security
  * For student educational records
* **Data breach notifcation Laws** - International, but differ per jurisdiction
  * Procedure to follow in case of data breach.

### Compliance Reporting
* **Internal/External reporting** to maintain transparency within the organization and with (external) stakeholders.
* **Internal** mostly for decision makers to see whatever needs to happen and make decisions
* **External** mmandated by regulary bodies or on request.
* **Proof** of commitment and current status

### Consequences of Noncompliance

* **Financial Penalties** like GDPR
* **Sanctions** like restricted business operations
* **Reputational damage** people might loose trust
* **Loss of business or contractual impacts** sue for damage, termination of contracts

* Tips: Regular audits, training, effective communication channels

### Compliance Monitoring
* **Due Diligence** researching and undestanding legal/regulatory requirements and evolving laws.
* **Due Care** ongoing efforts to ensure policies/controls are effective and maintained.
  * **Acknowledgement** - ensuring employees and partners are aware of the compliance requirements.
  * **Attestation** - Aware and comfirmed they adhere to the policies
* **Internal Monitoring** - preferabl automated where possible. Reduces risk, timely catching of issues, etc...

## Adopting Standard Frameworks
### NIST Cybersecurity Framework (CSF)
* **National Institute of Standartds and Technology (NIST)** develops cybersecurity standards across US federal government, but is published and many companies might use it.
* **Goals of CyberSecurity Framework (CSP)**
  * Describe current security posture.
  * Describe their target state for cybersecurity.
  * Identify & Prioritize oppertunities for improvement within the context of a continious and repeatable process.
  * Assess progress toward the target state.
  * Communicate among internal and external stakeholders about cybersecurity risk
* **3 Components**
  * 1. *Framework Core* the 5 functions - indentify, protect, detect, respond, and recover.
  * 2. *Framework Implementation Tiers* or rather the "maturiry model" that describes a level if implementation
    * - Tier 1: Partial
    * - Tier 2: Risk Informed
    * - Tier 3: Repeatable
    * - Tier 4: Adaptive
  * 3. *Framework Profile* how it might approach security functions

### NIST Risk Management Framework (RMF)
* **Mandatory for all Federal Agencies**
* Process to select, implementm and asses risk-based security and privacy controls.
* Less commonly used in private organizations.

### ISO Standards
* **ISO 27001** - Security
  * Implementation of a Information Security Management System (ISMS)
  * with 14 categories of **Control Objectives**
    * Information Security Policies
    * ORganization of Information Security
    * Human Resource Security
    * Asset Management
    * Access Control
    * Cryptography
    * Physical and environment security
    * Operations securitylaws.
    * Communication Security
    * System acquistion, development and maintenance
    * Supplier relationships
    * Information Security Incident Management
    * Information security aspects of business continuity management
    * Compliance with internal requirements, such as policies and with external requirements, such as
* **ISO 27002** - Security
  * Extension on ISO 27001
  * A list of suggestions of actual/concrete security controls
* **ISO 27701** - Privacy controls, extension on 27001.
* **ISO 31000** - Guideline for risk management programs
  * Not specific to cybersecurity or privacy

### Benchmarks and Secure Configuration Guides
* **NIST/ISO are highlevel** don't give practical guidance on actually implementing security controls.
* **Benchmarks** are guides with practical and concrete guidance, remember the hardening benchmarks from Center For Internet Security, CIS.

## Security Awareness and Training
> Responsible for establishing, promoting and maintaining an information security training and wareness program to foster an effective security culture in their organizations.

### User Training
* **Various Training Techniques**
  * **Role-Based Training** - Based on your role, you get appropiate level of training. A sys admin needs more and different training than the maintenance guy.
* **User Guidance and training**
  * *Phishing simiulation* - on all levels
  * *Anomalous behavior recognition* - person recognizes risky, unexpected things
  * *Security Polices and handbooks* - provide users with info where they can find critical security documents.
  * *Situational Awareness* - Update users on security threats facing the organization so they can recognize it.
  * *Insidere Threats* - Remind insiders mmay pose a threat/risk also
  * *Password Management*
  * *Removeable Media/Cables*
  * *Social Engineering*
  * *Operational Security* - importance of protectice information during normal operations.
  * *Hybid/remote work evenironments* - Instruct on best practices, like VPN on public WIFI.
* **Training Frequency** - balance `time spend` vs `benefit`
  * Example: Training at onboarding and then annual refreshers
* **Development and Execution**
  * First asses the organzation for its security landscpae, risks and threats
  * Then tailor a training plan
  * Use real world examples
  * Execution
    * USe various methods (workshops, elearning, simulations, ...)
* **Reporting and Monitoring**
  * Track participation in trainings.
  * Asses knowledge with quices.
  * Collect feedback from the users
  * Review if materials are still relevant.
### Ongoing Awareness Efforts
> Less formal effors, like posters, oneliners, etc... they don't require commitment.
* Examples:
  * Posters
  * Videos
  * Emails
  * ...
