### 5.2: Custody and safekeeping of issuer signing keys

It is critical to not only keep signing keys safe from unauthorized access but also to effectively monitor signing activity to ensure that there are not access problems at the application level enabling credential signatures that are not properly authorized to occur. Equally important to keeping the signing keys safe is being confident that they keys have not been copied from the system. As OB3 signing moves from pilot to production usage, Edubadges should be able to say it is following industry recommended practices for key management and signing. Some notes on the state of this rapidly developing piece of the industry.

*   Cloud platform Key Management Services, such as AWS KMS are not yet compatible with Ed25519 keys and may not be able to generate the signatures within linked data proofs.
*   HashiCorp Vault (open source or in HashiCorp cloud) offers a Ed25519-compatible [sign API](https://developer.hashicorp.com/vault/api-docs/secret/transit#sign-data) via its “Transit” API. It might be compatible with the inner workings of a verifiable credentials system that needs to
*   Google Cloud Platform [supports](https://cloud.google.com/kms/docs/reference/rest/v1/CryptoKeyVersionAlgorithm) RSA and ECDSA on the non-NIST secp256k1 curve but not Ed25519.

**Recommendation**:

*   Make use of KSMs, preferably with [Hardware Security Modules (HSMs)](https://en.wikipedia.org/wiki/Hardware_security_module) if possible that prevent keys from leaving the device where authorized signing occurs. As a fallback, consider executing credential signing within a microservice specific to that opportunity, where all signatures are reliably logged, so that the potential security consequences of application vulnerabilities in the Django-based backend do not increase risk by allowing that application to load signing keys into memory.

---

| [Back to Index](ob3-edubadges/README.md)   |  [Previous Chapter 5: Edubadges Architecture Considerations](ob3-edubadges/50-edubadges-architecture-considerations.md) |    [Next Chapter 5.3: Workflows for consumer verification](ob3-edubadges/53-workflows-for-consumer-verification.md) |
| :--- | :---: | ---: |
