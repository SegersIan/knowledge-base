# Feature Toggles

*Note: Also known as Feature Flags.*

These are not necessarily architecture domain specific, but they allow for a smooth transition in evolutionary architecture. Especially the operational toggles require maybe some architectural consideration if they make sense. 

The following part is basically a summary of this awesome [Martin Fowler Entry by Pete Hodgson](https://martinfowler.com/articles/feature-toggles.html).

## Why Use?

* **Code Branch Management**: By shipping new code to production, hidden under a toggle, you can limit the amount of long-lived branches. Also known as *dark deployments*.
* **Test In Production**: Test features in production with a limited set of users. Allowing for A/B testing or canary releases.
* **Flighting**: Incremental roll out of new functionality.
* **Kill Switch**: Turn of certain functionality without redeploying, like a circuit breaker. When the load is to high, you can switch off certain features that are resource intensive (e.g. a recommendation service). 


## Categories

It can be tempting to lump all feature toggles into the same bucket, but this is a dangerous path. The design forces at play for different categories of toggles are quite different and managing them all in the same way can lead to pain down the road. It can be tempting to lump all feature toggles into the same bucket, but this is a dangerous path. The design forces at play for different categories of toggles are quite different and managing them all in the same way can lead to pain down the road.

[See Diagram](https://martinfowler.com/articles/feature-toggles/chart-4.png)

| Type | Description | Lifespan | Dynamism |
| ---  | ---         | ---      | ---      |
| **Release** | Allow incomplete and un-tested codepaths to be shipped to production as latent code which may never be turned on, allowing for trunk-based development of larger features and user stories. |Short - Days, Weeks<br><br>Release Toggles are transitionary by nature. They should generally not stick around much longer than a week or two. | Typically Static<br><br>Changing that toggle by rolling out a new release with a toggle configuration change is usually perfectly acceptable. |
|**Experiment**|	Used to perform multivariate or A/B testing. Each user of the system is placed into a cohort and at runtime the Toggle Router will consistently send a given user down one codepath or the other, based upon which cohort they are in. Commonly used to make data-driven optimizations| Short - Hours, Days, Weeks<br><br>An Experiment Toggle needs to remain in place with the same configuration long enough to generate statistically significant results. Longer is unlikely to be useful, as other changes to the system risk invalidating the results of the experiment.| Highly Dynamic<br><br>Each incoming request is likely on behalf of a different user and thus might be routed differently than the last.|
| **Operational** |	Control operational aspects of our system's behavior.<br><br>Example: rolling out a new feature which has unclear performance implications so that system operators can disable or degrade that feature quickly in production if needed.| Short to Long - Weeks, Months, Years<br><br>Once confidence is gained in the operational aspects of a new feature the flag should be retired. However it's not uncommon for systems to have a small number of long-lived "Kill Switches" which allow operators of production environments to gracefully degrade non-vital system functionality when the system is enduring unusually high load.<br><br>These types of long-lived Ops Toggles could be seen as a manually-managed Circuit Breaker.| Dynamic<br><br>The purpose of these flags is to allow operators to quickly react to production issues they need to be re-configured extremely quickly. |
| **Permission** | Used to change the features or product experience that certain users receive. A Canary Released feature is exposed to a randomly selected cohort of users while a Champagne Brunch feature is exposed to a specific set of users.| Long - Months, Years<br><br>When used as a way to manage a feature which is only exposed to premium users a Permissioning Toggle may be very-long lived compared. | Highly Dynamic<br><br>Each incoming request is likely on behalf of a different user and thus might be routed differently than the last. |


## Static vs Dynamic Toggles

* Dynamic: Toggles which are making runtime routing decisions necessarily need more sophisticated Toggle Routers, along with more complex configuration for those routers.
* Static: Can be a simple config file, no need for a sophisticated Toggle Routers

## Long lived vs Short Lived Toggles

* Short Lived: A simple if/else check on a Toggle Router would suffice.
* Long Lived: We need more maintainable implementation techniques.

## Implementation Techniques

Feature Flags seem to beget rather messy Toggle Point code, and these Toggle Points also have a tendency to proliferate throughout a codebase.

* De-coupling decision points from decision logic.
* Inversion of Decision.
* Avoiding conditionals.

## Toggle Configuration

* Dynamic Routing vs Dynamic Configuration: When highly dynamic, there is still a distinction between "Routing" (e.g. for user X, experiment/permission toggle is Y) and "Re-Configuring" (e.g. Disable feature x because of high server load). The dynamic routing logic itself in itself might have a configuration that is fairly static (e.g. the formula/algorithm that decides in which cohort users land for an experiment toggle).
* Prefer Static Configuration: Managing toggle configuration via source control and re-deployments is preferable, if the nature of the feature flag allows it. Managing toggle configuration via source control gives us the same benefits that we get by using source control for things like infrastructure as code and the code base itself.
* Approaches for managing toggle configuration: 
    * Hardcoded Toggle Configuration: Comment/Uncomment blocks of code. (requiring to rebuild and redeploy)
    * Parameterized Toggle Configuration: Commandline arguments or environment variables. (not requiring to rebuild, but requires redeploy or process restart)
    * Toggle Configuration File: Use a configuration file, could be part of more general application configuration. (not requiring to rebuild, but requires redeploy)
    * Toggle Configuration in App DB: Centralized database with configuration.  (not requiring to rebuild, nor requires redeploy)
    * Distributed Toggle Configuration: For HA, a database with configuration like Zookoper, etcd, or Consul.  (not requiring to rebuild, nor requires redeploy)
    * Overriding Configuration: You might have a defeault configuration (any from above) along with overrides based on a specific scope (e.g. Environment Specific, Per-request).

## Working with feature-flag systems

While feature toggling is absolutely a helpful technique it does also bring additional complexity. There are a few techniques which can help make life easier when working with a feature-flagged system.

* Expose current feature toggle configuration: Making is visible/accessible to know the current toggle configuration (e.g. dashboard).
* Take advantage of structured Toggle configuration files: Make human readable and understandable descriptions + maybe a contact person.
* Manage different toggles differently:
    * You might keep release toggles in your version control repo, but the operational toggles on a dynamic configuration.
    * Toggles can transition from category to category over time, which means you might need to refactor how the configuration is done. 
        * * E.g A feature toggle became a permission toggle.
* Feature Toggles introduce validation complexity (testing): Each toggle introduces new branches on the code baths. With multiple toggles in play we have a combinatoric explosion of possible toggle states. Happily, the situation isn't as bad as some testers might initially imagine. It is not necessary to test *every* possible combination. Most feature flags will not interact with each other, and most releases will not involve a change to the configuration of more than one feature flag.
* TIP: a good convention is to enable existing or legacy behavior when a Feature Flag is Off and new or future behavior when it's On.
* Where to place your toggle:
    * Toggles at the edge: Ideal for per-request context (Experiment/Permission Toggles)
    * Toggles in the core: Usually technical in nature, and control how some functionality is implemented internally. Localizing these toggling decisions is more sensible.
        * E.g. a Release Toggle which controls whether to use a new piece of caching infrastructure in front of a third-party API. 
* Managing the Carrying cost of Featue Toggles: Savvy teams view their Feature Toggles as inventory which comes with a carrying cost, and work to keep that inventory as low as possible

## Governance

Governance can be defined as the establishment of policies around the how/what/why/when of your feature flag implementation.

* **Limit Feature Flag Lifetimes to Minimize Technical Debt**: Based on their category/type, their lifecycle should be short or can be longer, make sure to follow this up.
* **Defining Access Controls for Flags**: Make sure that ignorant or unaware developers can flip the wrong switches. In addition, you might introduce some "2-step" verification, so another developer must approve your change of the feature toggle. This is more applicable in highly regulated industries.
* **Define, Document and Communicate Ownership Model**: Crisp ownership over who implements, rolls out, and maintains each flag must be absolutely clear. Some examples:
    * Most Common: The dev team owns implementation and maintenance; product team owns communication and the controls of the rollout.
    * Operational Flags acting as circuit breakers: DevOps or SRE may own the maintenance and communication.
* **Use TAGS if supported**: Tags are in the cloud world excellent metadata tools to tag any resources (like a feature toggle) with any arbitrary metadata that can help with the governance. E.g. The Owner, the category, description, maybe any dependencies.
* **Visibility**: We want visibility of feature flags, their state, and if possible, their interdependencies, their category, and their lifetime. Ways to do this:
    * Dedicated feature flag dashboard
    * Feature Flag dashboard integrated with your continuous delivery (CD).
* **Auditability**: The ability to audit the feature flags, when they existed and what their values were over time, who made these modifications, and who might have approved these modifications. Very useful to troubleshoot issues.
* **Policy As Code**: Leverage Policy As Code if available for your Feature Flag platform.

## Resources

* [Martin Fowler Entry by Pete Hodgson](https://martinfowler.com/articles/feature-toggles.html)
* [A feature flag horror story](https://dougseven.com/2014/04/17/knightmare-a-devops-cautionary-tale/)
* [Optimizely: Feature Flag Governance](https://www.optimizely.com/insights/blog/feature-flag-types-governance-optimizely/)
* [Azure App Configuration: Feature Management](https://learn.microsoft.com/en-us/azure/azure-app-configuration/concept-feature-management)
* [Feature Flags & Ephemeral Environments](https://www.qovery.com/blog/feature-flags-management-with-ephemeral-environments)