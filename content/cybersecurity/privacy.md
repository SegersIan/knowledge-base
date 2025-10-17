---
title: "Privacy"
---
# Privacy

* **Privacy Notice** - outlines the privacy commitments of an organization
  * In addition, also to their ToCs

## Data Inventory
> An overview of all types of information maintained by the organization, where it is stored, processed and transmitted.

* **Data Types**
 * **Personal Identifiable Information (PII)** - anything uniquely identifying individual persons (internal, external, customers, 3th party, employees, ...)
 * **Protected Health Information (PHI)** - Medical records from a health care provider or anyone under HIPPA.
 * **Financial Information** - personal financial records (some are under GBLA or PCI DSS relevant)
 * **Intellectual Property** - trade secrets like formulas, strategies, manufacturing process, ...
 * **Legal Information** - Documents regarding legal proceedings
 * **Regulated Information** - any data governed by LAW or REGULATION (HIPPA, PCI DSS...)
* Includes also non human readable data! (like binairy files)

## Information Classification
> Categorize data into classes based on sensitivity and impact, if it were to leak.

* **US Government Example**
 * *Top Secret* - could cause grave damage to national security - highest degree protection
 * *Secret* - could cause substantial damage to national security - substantial degree protection
 * *Confidential* - could cause some identifyable damage to national security - Some Protection
 * *Unclassified* - does not meet any other classes, but not possible to publicly share without authorization
* **Private Example**
 * *Public*
 * *Private*
 * *Sensitive*
 * *Confidential*
 * *Critical*
 * *Restricted*
* **Goal** - Allows distinct security roles for various different classes. DLP (Data Loss Protection) could really use this.

## Data Roles and Responsibilities

* **Data Ownership** - Designated specific ownerships/accountability for a type of of data/inforation
  * Example: Head of HR, all employee related records
  * Example: Head of Sales, all customer information
  * Data Owner Might delegete responsibility to others.
* **Data Privacy Roles**
  * **Data Subjects** - individuals whose personal data is being processed
    * Have often right to deletion of data, request data, access, correct, ...
  * **Data Controllers** - entities that determine the reasons for processing personal information and the methods. (kind of the data owner, but doens't have to have an interest)
  * **Data Stewards** - individuals who carrout out work for Data Controller and are delegated responsibility.
  * **Data Custodian** - responsible for secure safekeeping of the information but are neither stewards or owners of the data-
    * Example: A cloud service provider hosting customer data for a bank.
    * Exammple: A university’s database administrator maintaining student records.
  * **Data Processors** service providers that process data on-behalf of a data controller.
    * Example: Credit card processor on behalf of a reseller
  * **Data Protection Officer (DPO)** - overall responsibility for data privacy efforts

## Information Life Cycle
> Protection of data must happen through entire lifecycle of the data.

* **Data Minimization** - Collect smalles possible amount of data necessary to meet business requirements.
  * Unnecessary information should never be collected in the first place
* **Purpose Limitation** - Data should be only used for the purpose that it was originally collected for and that was consented by the data subject.
* **Right to Be Forgotten/erasure (GDPR)** - A data subject has the right to be forgotten and request this withing a reasonable timeframe, under certain circumstances:
  * The data no longer is needed for its original purpose
  * The individual withdraws consent
  * The individual objects, so no oveeridin legitimate interest
  * The data has been unlawfully processed
  * tere is legal obligation to erase the data
  * Note: Incorrect information can be harmful or misleading
* **Data Retention** - should be in place so it's clear when and for how long data is kept.

## Privacy Enhancing Technologies
> True anonymization is hard, but we can try pseudo anonymization techniuqes. This process is data obfuscation.

* **Data Obfuscation** tools
  * **Hashing** - Use the hash value instead of the identifyable information - sensitive to rainbow attacks, so the attacker should never have access to all records, else they can built such a table.
  * **Tokenization** - Replace sensitive values with randomly generated values. then there is protected lookup table incase identification is important.
  * **Data Masking** - Replacing all values with character except for last, like a creit card `**** **** **** 1234`

## Privacy and Data Breach Notification
> In case of a data breach, right regulatory bodies and stakeholders should be notified. Sometimes the affected data subjects should be also informed.
> some jurisdictions might require also public notification

## Tools

* https://privacybadger.org/
