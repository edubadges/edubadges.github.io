### 7.3: Feature flags and experimental tags

A feature flag, sometimes called a [feature toggles](https://en.wikipedia.org/wiki/Feature_toggle), is a capability of software to run either with or without a certain feature enabled. Advanced versions of this idea within Software as a Service involve selective enablement of features for certain audiences. This is one method to enable testing of experimental functionality without disrupting the experience of other users that do not use that functionality. It is important to maintain adequate testing across all options of how software can be run in production. Feature flag usage can dramatically increase the complexity of testing, and when automated testing is not available, this can be time consuming. Maintaining many feature toggles over time sometimes results in code that is littered with conditional statements. Some projects make feature flags a core part of their development philosophy, separating feature releases from code releases with [feature-flag driven development](https://featureflags.io/) and making use of configuration software or interfaces specifically developed for feature flag management or A/B testing.

Feature flags may be useful for OB 3.0 if it is valuable to run a pilot with only a subset of member organizations. But the added complexity, especially when there is not a centralized paradigm for how feature flags are managed. Here are stories that could lead to a feature flag enabling badges to be accessible in OB 3.0 format for a particular issuer:

*   As an Edubadges admin, I can select whether an issuer has edubadges enabled by selecting a choice for the `ob3_enabled` field from choices `Enabled`, `Disabled`, and `Default`.
*   As an Edubadges admin, I can configure the overall enabled status for an environment (either through application settings, or by changing a feature flag `ob3_enabled_default`.)
*   As a learner who has earned a badge from an issuer, if that issuer is in an OB 3.0 pilot, or the pilot has ended and all issuers are enabled for OB 3.0 (and this issuer has not specifically disabled access), I can download my badge in OB 3.0 format.

An alternative that allows all users of a particular release to try out OB 3.0 without finding confusion when they reach a dead end may be to label verifiable credentials as some form of experimental in the interface. Here are stories that could implement this idea:

*   As a learner who has earned an edubadge, I can see options to share my badge via URL. I can also see an option to “Download signed edubadge” with a lightly colored label “advanced”.
*   I can see that the “advanced” label is a clickable link that opens documentation in a new tab. I can get information about OB 3.0, and a suggestion of a couple things I could do with my downloaded badge, like services that accept import of OB 3.0.

---

| [Back to Index](ob3-edubadges/README.md)   | [Previous Chapter 7: Appendix A: User Stories and Milestones](ob3-edubadges/70-appendix-a-user-stories-and-milestones.md)    | [Next Chapter 7.4: Continued support for URL sharing and 2.0 verification](ob3-edubadges/74-continued-support-for-url-sharing-and-2-verification.md) |
| :--- | :---: | ---: |