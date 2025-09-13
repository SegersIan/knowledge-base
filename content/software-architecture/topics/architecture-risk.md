# Architecture Risk

Every architecture has risk associated with it. Analyzing risk is one of the key activities of architecture. By analyzing risk, the architect can address deficiencies within the architecture and take corrective action to mitigate the risk.

## Risk Matrix

When assessing architecture risk it's hard and fairly subjective to qualify a risk as *low*, *medium*, or *high*. The risk matrix can be leverages to reduce the level of subjectiveness.

The architecture risk matrix uses 2 dimensions to qualify risk: the overall impact of the risk and the likelihood of that risk occurring. Each dimension can be qualified as *low (1)*, *medium (2)*, or *high (3)*. These numbers are multiplied together within each grid of the matrix, providing an objective numerical representation of that risk.

* Risk 1 - 2 : Low Risk (green)
* Risk 3 - 4 : Medium Risk (yellow)
* Risk 6 - 9 : High Risk (red)

**TIP: Considering to start first with the "overall impact" dimension before rating the likelihood**.

### Matrix

| Overall Impact / Likelihood Of Risk | Low (1) | Medium (2) | High (3) |
| --- | --- | --- | --- |
| Low (1) | 1 (green) | 2 (green) | 3 (yellow) |
| Medium (2) | 2 (green) | 4 (yellow) | 6 (red) |
| High (3) | 3 (yellow) | 6 (red) | 9 (red) |


[Colored Risk Matrix](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2001.png)

### Example

There is a concern about availability with regard to a primary central database used in the application:
* **Overall Impact**: Loosing the databases has a **high impact** if the application needs the database to do anything.
* **Likelihood Of Risk**: If the database is Highly Available in a cluster configuration, then there is **a low likelihood of risk**.
* **Overall Risk Rating**: High (3) * Low (1) = 3 (Medium Risk)

## Risk Assessments

Given that we have the risk matrix to help grade risk, we can make a summarized report of the overall risk of an architecture. That is what we call a risk assessment.

| Risk Criteria | Customer Registration | Catalog Checkout | Order Fulfillment | Order Shipment | Total Risk |
| --- | --- | --- | --- | --- | --- |
| Scalability | 2 | 6 | 1 | 2 | 11 |
| Availability | 2 | 4 | 2 | 1 | 10 |
| Performance | 4 | 2 | 3 | 6 | 15 |
| Security | 6 | 3 | 1 | 1 | 11 |
| Data Integrity | 9 | 6 | 1 | 1 | 17 |
| Total Risk | 24 | 21 | 8 | 11 |  |

Such a Risk Assessments allows to find critical areas that need attention and prioritize accordingly, by looking at the risk by domain or criteria. Based on the business and domain, certain criteria or domains will have priority over the others (e.g Checkout might be considered the most critical for some businesses).

Risk assessments should be done periodically, as these are not static factors. Measure them over time and track the trends of the values. Annual risk assessments are a good starting point.

### Visual Variations for better story telling
* [Risk Assessment - Normal](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2002.png)
* [Risk Assessment - Highlighting high risk](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2003.png)
* [Risk Assessment - Direction of risk with +/- symbols](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2004.png)
* [Risk Assessment - Direction of risk with arrows and numbers](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_2005.png)

### ISO 27001 & Security

Doing risk assessments is considered a best practice for security. The ISO 27001 information security standard has one of its central tenets the process of doing periodical risk assessment.

## Identifying Risk

There are various methods to **identify and address** risks in your architecture. 

|     | [Threat Modeling](threat-modeling.md) | Risk Storming |
| --- | ---             | ---           |
| **Definition** | - Systematic Process<br>- Can be done collaborative but emphasize is on the process. | - Collaborative Technique  |
| **Participants** | Usually security experts | Various stakeholders, from developers to business analysts to users |
| **Scope** | Primarily focused on security threats  | Looks at a broader rang of risk, which can include security, but also usability, performance, compliance, and other concerns. |
| **Output** | Typically results in a list of potential threats, their severity, and suggested mitigation strategies. | Outputs not only a list of risks but also a prioritized set of actions based on the collaborative discussions. |
| **Notes** | Strong security emphasize | Might also result in a better understanding of business priorities, user concerns, and technical constraints.

[Threat Modeling](threat-modeling.md) deserves its own place, so we will cover here only Risk Storming.

## Addressing Risk

Once risks/threats are identified with their respective risk rating, identified risks can be addressed in various ways:
* **Avoid Risk**: Stop doing the activity that causes the risk.
    * Example: Delete the web server if it's not used anymore.
* **Mitigate Risk**: Implement controls or measures to reduce impact or likelihood.
    * Example: Move a database to a High Available cluster configuration.
* **Transfer Risk**: Transfer the risk to a 3th party.
    * Example: Buy insurance, outsource activity, ... When using Azure, you transfer any risk regarding physical server security to Azure.
* **Accept Risk**: We don't do anything, and accept consciously this risk. Usually when measures/controls would outweigh the risk. Or the risk is just too low.
    * Example: The risk rating is to low
    * Example: Special software would cost $100 000, while your company has revenue of $20 000.

## Risk Storming
Risk storming is a collaborative exercise used to determine architectural risk within a specific dimension. Common dimensions (areas of risk) include unproven technology, performance, scalability, availability (including transitive dependencies), data loss, single points of failure, and security. Risk storming efforts include architects, senior developers, and tech leads. Providing an implementation perspective for architects, but also for non-architects to gain a better understanding of the architecture.

Risk storming involves an individual part and a collaborative part. An architecture diagram is used for both parts. Based on the scope of the risk storming (entire architecture or a specific context) appropriate architecture diagram should be provided.

### Step 1: Identification (individual)
Each participant  identifies areas of risk within the architecture on their own. This is essential so that other participants don't influence each other or direct attention away. This should be done ahead of time before the collaborative part starts. This preparation can be done with a risk per post-it, which is color-coded based on the overall risk rating (e.g. High - red). This means that each participant must rate each risk using the risk matrix ahead of time.

### Step 2: Consensus (collaborative)
The goal is gaining consensus among all participants in a meeting regarding the risk within the architecture. Ideally the architecture diagram is printed or visible on a large screen and at the start of the session, all participants put their post-its on the diagram, based on where they identified the risks.

Once all post-its in place, the collaborative part on gaining consensus in terms of the risk qualification. All post-its should be covered.

### Step 3: Mitigation (collaborative)

Now risks must be addressed, some will be mitigated, others might not, see [Addressing Risk](#addressing-risk) about what options exist. Key (business) stakeholders should be involved on deciding how risks are addressed as they are usually best positioned to decide on accepting risk or accepting costs to mitigate a risk.

## Example: Risk Storming

## Example: Complete Risk Assessment Table

| ID  | Risk | Overall Impact | Likelihood | Rating | Address | Notes |
| --- | ---  | ---            | ---        | ---    | ---     | ---   |
| 001 | Database becomes unavailable | High | Medium | High | Mitigate Risk | Configure Database as HA with cluster configuration |
| 002 | Hardware accessed by unauthorized person | High | Medium | High | Transfer Risk | Azure is responsible for hardware security |
| ... | ... | ... | ... |.... | ... |... |

## Resources

* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 20 - Contains Risk Story Examples
* [ISO 27001: Information Security](https://www.iso.org/standard/27001)