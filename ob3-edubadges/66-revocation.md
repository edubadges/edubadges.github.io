### 6.6: Revocation

The ability to mark a credential as revoked is an important capability for many Open Badges issuers, and is a feature of the Edubadges platform’s implementation of OB 2.0. With 3.0 shifting from hosted to signed verification, revocation checking must be done differently at a technical level, but the meaning remains the same. The VC Data Model offers an extensible mechanism by which a [credential status](https://www.w3.org/TR/vc-data-model/#status) resource may be exposed within a credential. Various use cases and solutions have been developed to enable credential status checking with a range of capabilities and implications. OB and CLR reference optional 1EdTech extensions supporting verifiers in obtaining updated representations of credentials and checking for revocation. Issuers and verifiers need to support a common mechanism in order for status checking to work, and yet issuers often need to produce the credential without knowing which other parties might someday rely on it or what methods those verifiers may support. Here are some mechanisms identified by the implementing community for status and revocation management.

*   The [1EdTech Revocation List Status Method](https://imsglobal.org/spec/vcrl/v1p0/) accompanies the OB and CLR specifications. This enables verifiers to query for status results without revealing to the issuer which specific credential’s status is being checked. It does reveal to the requester a list of credential IDs claimed by the issuer to be associated with it, though it is not assumed to be exhaustive or accurate except to indicate the status of the credential known to the requester, because issuers may use multiple lists concurrently, packaged with different sets of credentials and red herrings may appear in some lists. The 1EdTech certification process and validator software will support this status checking method. A reason for revocation may be available for a revoked credential.
*   Another option in the space, more on the Verifiable Credentials side of the ecosystem is the [Credential Status List 2021](https://w3c.github.io/vc-status-list-2021/) specification, which was adopted as a standards-track specification by the VCWG on December 14th 2022. This protocol enables an issuer to publish a compactly encoded list of status indicator bits covering many credentials at once in an unnamed order. Within each issued credential, the issuer includes a pointer to a specific bit within the bulk status list. This enables verifiers to efficiently query for status results without revealing which specific credential’s status is being checked. It does not feature the ability to retrieve a revocation reason for a revoked credential, nor does it provide a refreshed version of the credential consistent with the issuer’s latest status data, features that are sometimes bundled with revocation.

A related topic to Revocation is refreshing credentials. This covers use cases such as state changes for a credential other than revocation, including the addition of more data and renewal of expiring credentials by extension or replacement. This was a capability inherent to hosted verification that is also not automatically available when the credential format switches to signed portable JSON. The [1EdTech Refresh Service Method](https://imsglobal.org/spec/vccr/v1p0/) also accompanies the OB and CLR specifications and enables fetching of an updated version of a credential under inspection by a verifier. The 1EdTech verifier tools will request updated version if such an endpoint is indicated in the badge. There is no approach to authentication or variable authorization defined in this specification, so if an issuer uses it, it is presumed that any client could request the latest version of the credential from this endpoint if they knew the correct URL. Future versions of this specification may serve use cases that require more in-depth protection of refresh endpoints.

The 1EdTech Revocation List Status Method is the only of the above technical options that could be checked during conformance testing, but it does not appear that this will appear as an independently filterable line item in the [TrustEd Apps Directory](https://site.imsglobal.org/certifications). The selection of which mechanism should be used for revocation, like many other aspects of tech stack choices in OB 3.0, depends on the capabilities of the most important consumers for this data. The safest choice in this space is to implement the 1EdTech Revocation List method because of the known consumer, 1EdTech themselves. But if other specific consumers are prioritized coming from the Verifiable Credentials community more broadly, they are more likely to request the Credential Status List 2021 option. Several more months of observation of products coming online in the market will provide useful information about the relative benefits of each approach.

Either of the revocation list methods described here is delivered as an API endpoint offered by the issuer platform much like any OB 2.0 verification endpoint, except that OB 3.0 revocation lists are presumed to include multiple credential statuses in one list. Instructing issuers to report on multiple credentials presented in one list serves an occasionally-mentioned privacy goal where it is proposed that learners may prefer if issuers are not specifically informed when or how often credential consumers are verifying any particular credential. From the issuer platform’s perspective, a client request to verify any particular Open Badge in a list looks the same, and it is not possible for that platform to track users precisely. Having only one endpoint per issuer though would strain under the weight of a massive number of assertions if Edubadges implemented the 1EdTech option. It would be more minimal file sizes if Edubadges implemented the more technically complex Status List 2021 way. The technical differences are likely not as impactful as the consumer-based reasons one approach or the other would be favored.

If the desired strategy for generating signed `OpenBadgeCredential`s is through using [ORCA](#orca---open-recognition-community-app), publishing revocation lists is under the scope of responsibility of that microservice.