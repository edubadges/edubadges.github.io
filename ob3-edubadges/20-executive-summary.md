## 2: Executive Summary

After more than 12 years of exploration of the digital credentials landscape, the Open Badges Specification 3.0 release is underway. This includes a large realignment toward cryptographic verification and a step towards compatibility within a broadening digital credentials ecosystem through the adoption of the Verifiable Credentials Data Model, a W3C recommendation.

Edubadges can reach new audiences in coming years through updating its implementation of Open Badges from 2.0 to 3.0. But the ecosystem is not yet well developed, and it will take time for reliable credentials transfer pathways to provide real value for students. This means both that Edubadges does not find itself in a hurry to update to the new version of the specification and that the existing pathways for sharing achievements via URL should be maintained and supported.

A balanced path through pilots to a production launch of next-generation digital credentials looks like this:

*   Continue supporting OB 2.0 verification.
*   Continue supporting URL based sharing, and add credential value enabling users to add Edubadges to LinkedIn profiles, the current most consequential sharing destination.
*   Simplify the Edubadges service architecturally, and address tech debt.
*   Pilot 1: Add new OB 3.0 issuer support, achieving 1EdTech’s Issuer certification role, but do not yet implement the optional API.
*   Pilot 2: Observe the Verifiable Credentials / Open Badges ecosystem, choose a wallet partner in this space, and implement a connection protocol and user workflow for this wallet.
*   Pilot 3: Observe the development of European digital identity wallets, and consider delivering an integration with a promising option here as an alternate delivery path for the same achievements.
*   Transition service out of pilot: Complete refinements of the user experience, and launch successfully piloted features to all users, with focus on partners that consume edubadges.

Architectural improvements and simplifications are an essential part of a production service, and they also enable further pilot experimentation. Investing in reducing outstanding tech debt extends the potential life of the product by making it easier to execute pivots based on learning in the pilots. Removing features is difficult, but a product’s focus improves its potential for impact long-term.

Implementing OB 3.0 requires a significant amount of work, and it requires new security considerations. One option that may reduce costs for Edubadges is integration with ORCA, a forthcoming open source OB 3.0 issuing microservice under development by Skybridge Skills and partners. It implements an approach to Open Badges compatible with the recommendations laid out in this report. Risks and benefits of OB 3.0 delivery through a specialized microservice are presented.

Edubadges is poised to be a leader in the digital credentials ecosystem, because it is open source, and because it has a chance to set a pattern for how Open Badges are implemented in the European higher education market. Building momentum in a credential-consuming community around a particular set of technology and user experience choices will be critical in attracting valuable services to this ecosystem. In order to achieve maximum impact, the open source offering must be simple enough to have value for institutions outside of SURF’s network and the credentials must flow to destinations where learners can leverage them to open new opportunities. OB 3.0 and European digital identity initiatives change the landscape Edubadges must navigate to achieve these goals, but SURF’s plan to pilot capabilities and then move to production is the right plan for these challenges.

---

| [Back to Index](ob3-edubadges/README.md)   | [Previous Chapter 1: Introduction](ob3-edubadges/10-introduction.md)     | [Next Chapter 3: The Open Badges and Digital Credentials Landscape](ob3-edubadges/30-the-open-badges-and-digital-credentials-landscape.md) |
| :--- | :---: | ---: |
