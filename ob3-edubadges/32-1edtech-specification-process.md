### 3.2: 1EdTech specification process

1EdTech has published Open Badges and CLR as “Candidate Final Public”. The final specification will be released with few further changes after initial implementers are successfully tested for conformance. This is estimated to occur around the end of Q1 2023, but implementation may begin now.

As the 1EdTech test suite is in development, implementers should pay close attention to the specific requirements for testing, so that they can efficiently meet the requirements of those tests.

Services implementing Open Badges fall into one or more ecosystem roles, depending on their relationship to issued credentials. These roles are named “Issuer”, “Host”, and “Displayer”. Edubadges is closest to both Issuer and Host roles.

*   Issuer: A product that issues Open Badges and transmits them to learners. Certification as an issuer covers whether a well-formed signed `OpenBadgeCredential` is produced by the tested product.
    *   Optional API support: Issuers can achieve an additional level of certification for Issuer API support if they can demonstrate successful registration with the reference Host system, authorization code grant flow execution for a test user, and transmission of signed Open Badge(s) to the reference Host system by posting them to the Host API. Edubadges has not yet implemented this API, and it would be of medium difficulty. The [3.0 migration use case details](#how-to-publish-badges-in-ob-3.0) and [user stories](#enable-access-to-edubadges-in-ob-3.0-format) recommended in this report do not propose immediate adoption of the OB 3.0 API, but instead to prioritize this API implementation based on when important consumers may be connected to Edubadges
*   Host: A product implementing the server side of the Open Badges API that holds badges on behalf of data subjects or holders and controls API access to them. The Resource Server responds to automatic registration requests, authorization grant flow initiations, and authenticated resource requests via the API endpoints.
*   Displayer: A product that implements the client side of the Open Badges API. Certification is granted that the product can demonstrate successful registration with the reference Host system, authorization code grant flow execution for a test user, and transmission of signed Open Badge(s) from the reference Host system by making a request for credentials held by a user who completed the authorization flow.

The first hurdle to complete in adopting OB 3.0 is the issuer only (no API) certification. This covers significant scope and is recommended as the primary path Edubadges explore in its first phase of OB 3.0 implementation.

---

| [Back to Index](ob3-edubadges/README.md)   | [Back to Chapter 3: The Open Badges and Digital Credentials Landscape](ob3-edubadges/30-the-open-badges-and-digital-credentials-landscape.md) |    [Next Chapter 3.3: Comprehensive Learner Record (CLR)](ob3-edubadges/33-comprehensive-learner-record-clr.md) |
| :--- |  :---:  | ---: |