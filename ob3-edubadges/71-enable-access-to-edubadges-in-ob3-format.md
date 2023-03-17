### 7.1: Enable access to edubadges in OB 3.0 format

See examples and [use case details](#how-to-publish-badges-in-ob-3.0) in the previous section.

Existing OB 2.0 verification endpoints and features should remain in operation:

*   The Assertion verification endpoint, e.g. `https://api.edubadges.nl/public/assertions/a41jSgmsSh6Sa1xcVUku5Q` should continue to serve OB 2.0 data.
*   The BadgeClass (Achievement) endpoint, e.g. `https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g` should continue to serve data about the achievement and its criteria in OB 2.0 format. Observe recommendations made in the OB 3.0 implementation guide (see [draft](https://github.com/1EdTech/openbadges-specification/pull/501)) for “migrating from OB 2.0” to see if the community adds recommendations around combined representations of OB 2.0 and OB 3.0 data
*   The Issuer (Profile) endpoint. e.g. `https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg` should continue to serve data about the issuing organization in OB 2.0 format.

Learners can access OB 3.0 serializations from new features in the interface.

*   As a learner who has earned several edubadges, I can view the details of one of them, and I see that there is an advanced or experimental option to download in Open Badges 3.0 format.
*   When I select the download option in my browser, I am offered to save a `.json` file to my device.
*   The JSON of a downloaded badge is compliant with the Open Badges 3.0 data model, including a proof method named in the specification. It appears valid when verified by a 1EdTech verifier tool, when such a tool is available.

New technical capabilities are available for the above stories to be made possible.

*   The downloaded file is in Verifiable Credentials format, with an issuer identified by a `did:web` identifier with a path, such as `did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg`. This DID URL results in verification API requests to `https://edubadges.nl/issuers/lQ67BQQQS-eBx5syJGpazg`, which should respond with a DID document containing identifying properties in the OB 3.0 context and the Ed25519 keys used by this issuer, either directly or by redirecting to a local microservice responsible for signing and key management, such as [ORCA](#orca---open-recognition-community-app). See example in [use case details](#how-to-publish-badges-in-ob-3.0).
*   The credential is signed using a signing key held by the Edubadges service on behalf of the issuer.

It is almost certain that Edubadges users among SURF member institutions will not want to lose the capability to revoke badges, but this does require the publication of a new status list resource for one or more sets of credentials.

*   As an issuer, I can revoke a previously awarded edubadge. It will no longer be valid when attempts are made to verify it. It will appear as revoked in a [revocation list](#revocation) for the issuer.

---

| [Back to Index](ob3-edubadges/README.md)   | [Previous Chapter 7: Appendix A: User Stories and Milestones](ob3-edubadges/70-appendix-a-user-stories-and-milestones.md)    | [Next Chapter 7.2: Wallet integration and recipient identifiers](ob3-edubadges/72-wallet-integration-and-recipient-identifiers.md) |
| :--- | :---: | ---: |