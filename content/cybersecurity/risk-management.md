---
title: "Risk Management"
---
# Risk Management and Privacy

## Analyzing Risk

* **Enterprise Risk Program (ERP)** - Formal approach to risk analysis
  * 1. Identify Risks
  * 2. Depetermine severity for each risk
  * 3. Adopt risk management strategies to address risks
* *Clarification*
  * **Threats: any possible events that might impact CIA characteristics**
    * The Bad Guy/Thing: It’s something that might cause trouble. Like a burglar who wants to break into your house.
  * **Vulnerabilities: weaknesses in our systems/controls that could be exploted by a threat**
    * The Weak Spot: It’s the thing that makes it easier for the bad guy. Like if you left the window unlocked.
  * **Risk: Overlap between of Threats and Vulnerabilities**
    * What could actually happen: It’s the chance of the bad guy using the weak spot to cause harm. Like the burglar actually climbing through your unlocked window and stealing your toys.
* ![img](../assets/risk_mgmt_vendiagram.jpg)
  * A **threat** that has no corresponding **Vulnerability** to exploit, results in no **risk**.
* *CyberSecurity Example*
  * Threat - An attacker with a brute-force tool
  * Vulnerability - Expose port 22 for SSH
  * Risk - The commbination is the risk.

### Risk Identification
> Identify **threats and vulnerabilities** in your operation environment/scope/boundary

* **External Risks** - from outside organization
* **Internal Risks** - from inside organization
* **Multiparty Risks** - Impacts more than one organization (e.g. Power Outage for entire city)
* **Legacy Systems** - outdated systems that don't receive updates, patches, etc...
* **Intelectual Property (IP) theft Risk** - Organization's IP that, when disclossed, impacts business advantage
* **Software Compliance/Licensing Risk** - intentional/accidental breach of ToS/License cause Financial and Legal Risk.

### Risk Assessment
> Not all risks are equal.

* *We asses risk on 2 dimensions*:
  * **Likelihood** of it occuring, aka the probability.
    * Possible way of expressing `10% chance of happening this in the next year`
  * **Impact** if it occures
    * Possible way of expressing `financial cost of 100 000 EUR`
* **Risk Severity = Likelihood * Impact**
  * This is mostly conceptual, doesn't habve to be dine literally.
* **Ways of performing Risk Assesment**
  * *One-Time* - Snapshot of specific time, often in response to a security incident.
  * *Ad-hoc* - in response to specific event/change, like an new project, tech...  . Often quickly to adress a certain set of concerns.
  * *Recurring* - on regular base, to track evolution of risks
  * *Continious* - on continious base through automation and tooling

### Risk Analysis
> Formalized approach to risk prioritization in a structured maner.

* **2 Methodologies**
  * **Quantitative Risk Analysis** - Use numeric data  in the analysis, allows for straightforward prioritization,
  * **Qualitative Risk Analysis** - Use subjective analysis, more difficult.
  * Not uncommon that they are combined.

#### Quantitative Risk Analysis
> Calculated for each threat/vulnerability combination

* **Determine Asset Value (AV)** - that is affected by the risk
* **Determine Annualized Rate Of Occurance (ARO)** - probability of the risk occuring annually
  * ARO of 2.0 => Probable that the risk occurs 2x per year.
  * ARO of 1.0 => Probable that the risk occurs 1x per year.
  * ARO of 0.01 => Probable that the risk occurs 1x per 100 year.
* **Detemine Exposure Factor (EF)** - relative value of the asset to be affected if the risk materializes.
  * EF of 100% => Entire Asset destroyed
  * EF of 50% => Half Asset destroyed
* **Calculuate Single Loss Expectancy (SLE)** - absolute value of the asset to be affected if the risk materializes.
  * Formula: `AV * EF`
  * Example: `1000 EUR * 50% => 500 EUR` loss if the risk materializes
* **Calculuate Annualized Loss Expectancy (ALE)** - absolute value of the asset to be affected if the risk materializes accordingly to annual probability.
  * Formula: `SLE * ARO`
  * Example: `500 EUR * 2.0 => 1000 EUR` loss if the risk materializes
  * Use **ALE** to prioritize, if it cost more to protect an asset than the value of its ALE, there is no point arguably to put in the effort.

##### Example
> You have an email server that sends out emails to customers and generates 1000$ in sales per hour.
> Can happen up to 3x year to have a DDoS attack.
> It would take 3 hours to recover.
> When it happens, the email server would work only at 10% capacity.

* **AV** - $1000/hour
* **ARO** - 3.0
* **EF** - 90% (because the server works at 10% when experiencing the attack)
* **SLE** - `($1000/hour * 3h) * 90% => $2700`
* **ALE** - `$2700 & 3 => $8100`

#### Qualitative Risk Analysis
> Some risks don't qualify easily (e.g. Risk to Reputation)
* *We rate the risk on 2 dimensions* with a score of `low`, `medium`, `high`:
  * **Magnitude**
  * **Probability**
* *Risks with `high` magnitude and `high` probability should be prioritized*
* *Risks with `low` magnitude and `low` probability should be deprioritized*
![img](../assets/risk_mgmt_prob_mag.jpg)

### Supply Chain Assesment
> Don't forget to also do a risk assesment of your supply chain.

### Conclusion

* **Risk Analysis** provides guidance in prioritizing risk.
* **Quantitative Risk Analysis** helps determine if the cost to avoid a risk is justified.

## Managing Risk
> Once risk has been identified, assesed, analyzed/prioritized we can choose of the following 4 ways to manage/adress each risk.

### Risk Mitigation
> Apply security controls to reduce probability and/or magnutide.
* Per risk, you might apply multiple security controls to achieve mitigation.
* Examples:
  * Buy DDoS protection
  * Locks for laptops

### Risk Avoidance
> Change business pratices/systems to eleminiate the potential alltogether.
* Examples:
  * Just don't have laptops, if you don't want them to be stolen.

### Risk Transference
> Shifts (some of) the impadct to another entity
* Examples
  * Buy Insurance for stolen laptop
  * Buy "distinct cybersecurity insurance" cause default insurances don't cover this.
  * Use cloud servives, they take responsibility of the datacenters (hardware security)

### Risk Acceptance
> Don't do anything, accept the risk, the cost to avoid/transfer/avoid is bigger than the actual risk materializing.
* This is not neglicence, here we conciously, intentionally choose to accept the risk.
* Might require `Exemptions` or `Exceptions` on a policy to allow Risk Acceptance formally
  * `Exceptions` - cost is to high, organization accepts it thoughfully
  * `Exemptions` - more formal exceptions, may require high level approval and may come with an "end date".

## Risk Tracking
* **Inherent Risk** - original level of risk before any security controls were implemented.
  * Therefore, they are inherint to the business.
* **Residual Risk** - level of risk after implementing controls
* **Risk Appetite** - level of risk the organization is willing to accept
  * **Expansionary Risk Appetite** high risk, for high rewards. Typical for high growth organizations
  * **Neutral Risk Appetite** medium risk, medium rewards. Stability and growth is keu
  * **Conservative Risk Appetite** avoid high risk all together, prioritize security over high growth, risk averse.
* **Risk Threshold** - the specific threshold where the risk appetite stops and would trigger some actions
* **Risk Tolerance** - ability to whitstand risk and continue operations
* **Key Risk Indicator (KRI)** - metrics to measure increased level of risk.
  * Measures effectiviness of risk mitigations and makeing sure the risks stays within the appetite.
  * A Key Risk Indicator (KRI) is a metric that signals increasing risk exposure in an organization — like an early warning system for potential problems.
  * measurable signs that a risk might materialize or worsen.
* **Risk Owner** - Individual/entity responsible managing/monitoring risk and implementing controls.

### Risk Register
* The tool that tracks all the risks.
* Too communicate to leadership risk matrixes and heatmaps are often used.
* **To include: Risk Owner, RIsk Threshold information, KRIs.**

![img](../assets/risk_mgmt_impact_likelihood.jpg)

### Risk Reporting
> Communicating the status and evolution of risks to stakeholders.

* *Reporting Methods*
  * **Regular Updates** - routing reports to stakeholders with status, effectiveness of controls and changes
  * **Dashboard Reporting** - Real-time visual aids to summerize risk
  * **Ad Hoc Reports** - Created as needed
  * **Risk Trend Analysis** - Analyze history to indetify patterns/trends
  * **Risk Event Reports** - Document specific security events, like incidents

## Disaster Recovery Planning (DRP)
> Develop as soon as possible in case of disaster.
> Usually the key focus is a plan for each facility, as disasters often are scoped to a facility.

### Disaster Types (Examples)
* **Hurricans**
* **Floods**
* **Natural disasters**
* **human-made origin**
* **internal risk**
* ...

### Business Impact Analysis (BIA)
> Formal process to indentify mission essential functions in an organization and identify the systems that support those functions.

* **Mean Time Between Failures (MTBF)** - measure stability of a system, how much time between failures
* **Mean Time To Repair (MTTR)** - average time to restore operations after failure
* **Recovery Time Objective (RTO)** - Time you can tolerate the system being down
* **Recovery Point Objective (RPO)** - Amount of data you can tolerate to lose

* Note: Focus on `single-point-of-failure`
