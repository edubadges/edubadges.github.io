8: Appendix B: Resources
---------------------

The following resources provide more detail on specific topics. This list includes links to technical components of the Edubadges system as it exists today and information about the evolving digital credentials ecosystem.

*   [Open Badges 3.0 Candidate Final](https://1edtech.github.io/openbadges-specification/ob_v3p0.html)
*   [Comprehensive Learner Record 2.0 Candidate Final](https://1edtech.github.io/ComprehensiveLearnerRecord/docs/clr_v2p0.html)
*   [SURF wiki on Open Badges 3.0](https://wiki.surfnet.nl/display/EduCr/Background+information+about+OB3)
*   [Sphereon Open Source repos](https://github.com/Sphereon-Opensource)
    *   [ssi-mobile-wallet](https://github.com/Sphereon-Opensource/ssi-mobile-wallet)
*   [Signing Service](https://github.com/edubadges/signing-service) by SURF, integrated into edubadges-server for pilot testing of signed credentials anchored to blockchain transactions for trustworthy timestamping.
*   [EBSI DID Method](https://ec.europa.eu/digital-building-blocks/wikis/display/EBSIDOC/EBSI+DID+Method). Legal Entities (LE) can store DID Documents on the EBSI Ledger. Natural Persons DID Document (DID Method NP) derived from signed JWT. For natural person, method specific identifier is the multibase base58btc encoded representation of the version byte 2 plus the 32 byte sha-256 JWK thumbprint. It says “The resulting DID Document can be derived from Verifiable Presentation, after the proof assertion.”, and the verification method ID is indeed the JWK thumbprint within the DID document.
*   [EBSI trusted issuers registry docs](https://api-pilot.ebsi.eu/docs/apis/trusted-issuers-registry/latest#/)
*   Dutch Open Education API \[overview\]\](https://openonderwijsapi.nl/) and [API spec](https://openonderwijsapi.nl/specification/v5/docs.html)
*   [SURFeduhub](https://www.surf.nl/en/surfeduhub-secure-exchange-of-educational-data) is a platform for sharing educational data between Dutch educational institutions
*   [Documentation about Canvas LTI](https://wiki.surfnet.nl/pages/viewpage.action?pageId=70738038)
*   Design notes on SURF/eduID [EDU/SSI wallet project](https://wiki.surfnet.nl/display/SSI/Design+en+development+findings)
    *   [IRMA](https://irma.app/?lang=en) is a Dutch initiative for collecting and securely sharing “attributes”. No notes yet on Verifiable Credentials as a attribute attestation format.
    *   [Wallet UX demo/design](https://wiki.surfnet.nl/display/SSI/Resultaten+SSI+wallet+poc)
*   [VC-API draft specification](https://w3c-ccg.github.io/vc-api/) has not achieved official status within the Credentials Community Group, but there is some desire to publish it through that group as a non-normative draft report. Edubadges could act as an Issuer Coordinator connected to an Issuer Service/Status Service microservice responsible for signing credentials and keeping keys safe.
*   [eIDAS Toolkit for Businesses](https://digital-strategy.ec.europa.eu/en/news/eidas-toolkit-businesses) - toolkit is required to support methods chosen by any member country, will be expensive to build, but theoretically will support credential formats and transport protocol supported by Dutch government. See further notes in the [SURF wiki](https://wiki.surfnet.nl/display/EduCr/The+European+Digital+Identity+Wallet+Architecture+and+Reference+Framework).

---

| [Back to Index](ob3-edubadges/README.md)  | [Previous Chapter 7: Appendix A: User Stories and Milestones](ob3-edubadges/70-appendix-a-user-stories-and-milestones.md)
| :--- | :---: | ---: |
