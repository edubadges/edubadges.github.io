### 5.5: OB 3.0 as a microservice

An actionable strategy that could improve security is to refactor the OB 3.0 serialization responsibilities to deliver them as a microservice consumed by Edubadges. As an open source package, edubadges-server, even if it were upgraded to natively issue OB3 badges, does not serve an ideal role for other OB3 implementers beyond SURF for a couple reasons:

*   **Over-specificity**: The particular data relationships represented in the system are particular to SURF member universities, and both features and restrictions evident in the code are specific to SURF’s needs, such as the distinction between Edubadges and lower-tier badges and the verified names system that depends on eduID. If Edubadges is to take advantage of the opportunity to collaborate with other organizations on a secure general-purpose open source offering and then offer Edubadges as an open source badge management system that provides a range of workflows needed by higher education institutions.
*   **Security model** In production the Edubadges system relies on the `edubadges-server` application running on the [api.edubadges.nl](https://api.edubadges.nl/) domain as the source of truth for the existence of badge awards. Once upgraded to OB3, the integrity of the credentials depends on the security of signing credentials. The Django application `edubadges-server` has a much larger attack surface than necessary, given its pilot approach of storing credential signing keys in its database and signing credentials with those keys in memory. An approach to upgrading the security of the signing system to the level that would be suitable for production would be: refactor a narrow slice of the overall application functionality into a microservice focused on credential signing.

One implementation approach that would address the above concerns would be to develop core OB3 capabilities as a new microservice within the Edubadges system, like the `edubadges-ui` is separate from `edubadges-server` already. This would enable several potential benefits:

*   Reusability by other organizations. If the architecture of such a microservice can be clearly defined as a small thing for general purpose consumption, a critical mass of implementers could be built up around Edubadges-compatible architecture choices.
*   Software could more easily take advantage of key open source dependencies from the Verifiable Credentials ecosystem that can’t currently be used within `edubadges-server`. For example, [Digital Bazaar](https://github.com/digitalbazaar?q=vc&type=all&language=javascript&sort=) offers a number of open source packages in JavaScript to accomplish typical Verifiable Credentials tasks.
*   The existing Edubadges open source offerings could be more precisely targeted for external usage at Universities, and focus the offering more tightly on use cases around institutional management of credentials and student data. Not all consumers of a narrower core package would need these workflows, features, and restrictions.

---

| [Back to Index](ob3-edubadges/README.md)   |  [Previous Chapter 5: Edubadges Architecture Considerations](ob3-edubadges/50-edubadges-architecture-considerations.md) |    [Next Chapter 5.6: ORCA - Open Recognition Community App](ob3-edubadges/56-orca-open-recognition-community-app.md) |
| :--- | :---: | ---: |
