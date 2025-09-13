# Threat Landscape

## Threats
### Threat Characteristics
* Internal vs. External - Within or outside our organization.
* Level of Sophistication/Capability - from script kiddie to APT (advance persistant threat)
* Resources/Funding - from hobbyists to government funded
* Intent/Motivation - from "trill" to "warfare", from white to black hat
  * White Hat - Act with authorization and seek vulnerabilities with the intent of correcting them.
  * Grey Hat - Act without authorization, but seek to inform targets from found vulnerabilities.
  * Black hat - Act without authorization, with malicious intent.
### Advance Persistent Threat (APT) - Advanced attacks that persistent for a long time, stalking targets to attach when most strategic.
### Shadow IT - Indivduals/groups use technology/tools that are outside the approved solutions.
### Threat Actors
* Unskilled - (Script kiddie), little skill, depend on (automated) tools they downloaded, often don't understand how the tools work.
  * Do not underestimate this threat and risk
  * They often randomly take targets, and there are many.
* Hactivists - Want to reach an activist goal
  * Might take greater risk, cause their goal is more important than getting caught. Maybe even martyrdom.
* Organized Crime - Primairy goal is to make money
  * Like to be low profile, not get caught, it takes money to make money
* Nation-State Attackhers - Often do APT, it's all about strategic power and influence.
  * They often search for Zero-Day attacks and exploit them.
* Insider Threat - Employer, contractor, vendor or anyone with authorized access attacks the organization.
* Competitors - Corporate espionage

| Characteristic            | Unskilled | Hacktivists | Organized Crime | Nation-State | Insider | Competitor |
| ---                       | ---       | ---         | ---             | ---          | ---     | ---        |
| Internal/External         | External | External (mostly) | External | External | Internal | Both |
| Sophistication/Capability | Low | Any Level | Mid to High | High | Any | Any |
| Resources/Funding         | Few | Any range | Many | Many | Few | Many |
| Intent/Motivation         | Thrill/status | Ideals | Money | Economic/Espionage/Political | Varied | Economic/Business |

### Attaker Motivations
* Data exfiltration - desire to obtain sensitive/IP information.
* Espionage - organizations desiring to steal secret information
* Service disruption - Seek to stop opperations
* Blackmail - Seek to get money or concessions by threating to release secret info or more attacks.
* Financial Gain
* Ideoligy/Beliefs
* Ethical - White hat
* Revenge - just to embarrse or damage
* Disruption/chaos
* War - Manipulate the outcome of an armed conflict
### Threat Vectors and Attack Surfaces
* Attack Surface - A llsystem/application/service that could be potentially exploited
* Threat Vector - The actual vulnerability chosen from the attack service. The means to obtain that access.
* Message-Based - Email is most exploited attack vector.
  * They only need ONE person to be tricked.
  * Other channel: SMS, IM, Voice call, ...
* Wired networks - physically connecting to the on-prem network, or accessing a device that's connected to it.
* Wireless networks - Don't require physical access to the network, bluetooth is also a risk.
* Systems - Individual systems
* Files & Images - Infected files with malicious code that trigger once openend.
* Removeable devices - USB drives, Memory cars, trick anyone to put it in their computor.
* Cloud - Default configs, public access, of any cloud service.
* Supply Chain - Interfere with the organization's IT supply chain (e.g. infect OSS packages, patched hardware, ...)
  * Managed Service Providers (MSPs) often have special priviledge access to an organization's network.
  * Hard to adress and mitigate

## Threat Data & Intelligence

### Threat Intelligence: Resources and activities available to learn about changes in the threat environment.
* Can be used for predictive risk.
* OSINT tools/methods
* Vunerability databases
* Threat feeds
* Indicators of compromise (IoCs) - Like file hashes, signaturesm ,,,
### OSINT
* Key is to find up-to-date sources
* [Examples](./resources.md#Threat%20Feeds)
### Proprietary & Closed-Source Intelligence
* Might provide, better, curated and quality threat feeds
### Use multiple feeds - To cross check if any is slow or not updating
### Threat Maps - Geographic view of threat intelligence, but notoriously unreliable (VPNs, Proxies, ...)
### Assessing Threat Intelligence - regardless the source, assesment is required
* Is it timely?
* Is this information accurate? - Can you rely on provided information? Often correct?
* Is this information relevant? - Might not be relevant to your organization
* *Confidence Score* - Filter/assess data based on how much they trust it.
  * The lower the score, one should be cautious to make important decisions, but not ignore the source
  * The higher the score, the more trust and cofidence can go in major decisions.
* Many threat feeds provice a score. For example:
  * 90 - 100: Confirmed - multiple sources and direct analysis to confirm its true
  * 70 - 89: Probable - Depends on logical inference
  * 50 - 60: Possible - agreed with the analysis but assesment not confirmed
  * 30 - 49: Doubtful - Possible but not the most likey option, but there is no information that allows to disprove it
  * 2 - 29: Impropable - Possible but refuted by others
  * 1 : Discredited - Just plain not true
### Threat Indicator Management & Exchange - standerized communication protocals
* Structured Threat Information eXpression (STIX) - XML, a json variation exists
* Trusted Automated eXchange of Intelligence Information (TAXII) - communicate on HTTP level.
* [See Github](https://oasis-open.github.io/cti-documentation/)
### Information Sharing Organizations
* Industry-specific collaborative organizations that facilitate trusted human + machine
* Information Sharing and Analys Centers (ISACs) - for intrastructuree owners and operators
* [National ISACS](https://www.nationalisacs.org/)
### Conducting Your Own Research.
* Vendor security information sites
* Academic Journals and Technical Publications
* Conferences and meetups
* Social Media accounts of security professionals.
