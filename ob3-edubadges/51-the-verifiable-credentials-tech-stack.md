### 5.1: The Verifiable Credentials tech stack

The scope of the Open Badges 2.0 and 2.1 specifications covered data format, recipient identifier scheme, issuer identifier scheme, verification mechanism, file-based interchange format, RESTful API, and data schema. Now OB3 takes a role within a broader Verifiable Credentials ecosystem and specializes mostly in the data schema niche. This means that the community of organizations implementing OB3 take on a greater responsibility to choose the right options for the interoperability that they need.

There are challenges introduced by bringing Open Badges 3.0 into the VC ecosystem. Specifically, there are more implementation options that could result in a failure to interoperate between products, so identifying and pursuing specific high-value integrations early on is now more urgent. In addition, providing adequate fallback options for learners to gain access to opportunities is important in cases where technical interoperability of the VC objects themselves is necessary. End users who have earned Open Badges should not suffer a reduction of usability or shareability of their credentials when their issuer migrates to OB3.

Below are several independent layers of the VC stack where implementers have options within OB3

#### Proof type

The `Ed25519Signature2020` proof suite will likely be widely supported within the Open Badges community and certification test suite. It is a clear leading contender for an initial OB 3.0 pilot. If in later phases, the product needs to use a different proof type in order to get edubadges to other pools of consumers, additional serializations could be piloted to explore the value of those channels. For example, [some EBSI-endorsed signing mechanisms](https://ec.europa.eu/digital-building-blocks/wikis/display/EBSIDOC/E-signing+and+e-sealing+Verifiable+Credentials+and+Verifiable+Presentations) currently use a JWT VC format with a different kind of proof, an ES256 JWS (ECDSA). This curve is more widely used within cloud vendors secure secrets management services than Ed25519, and factors like this might lead the ecosystem to prefer something else over time.

As with all tech stack choices, particular attention should be paid to the target consumers for the badges. If Edubadges desires to serve consumers that are already integrating with other credentials in the EBSI ecosystem, that may mean that using compatible key and proof formats is not enough, it may also be necessary to produce credentials serialized for compliance with the European Learning Model. This may necessitate a separate serialization from the OB3 version, or it may be possible to deliver a unified signed credential that is compatible with both data schemas. The basic principle is that the achievement may be presented in various serializations, and modeling the capabilities of the consuming application is needed to determine the optimal path and the prioritization of different presentations.

**Recommendation**: Implement `Ed25519Signature2020` proofs for the first phase where Open Badges are available for download by users. After development of this initial capability, seek specific consumer destinations for credentials based on much each consumer might enable learners to leverage their edubadges into new opportunities. With specific next-stage consumers in mind, figure out what credential proof and wallet integration you might need to deliver (likely as a separate “serialization” of the same credential) in order to reach that audience.

#### Recipient identifiers

Presently Edubadges uses a learner’s eduID as the recipient identifier. When viewing a share URL, consumers are able to see the learner’s name and the validation status of that name through an institution as the primary mechanism of identity verification, and the eduID doesn’t enter the picture. At the level of the verifiable Open Badges if they were exported to another system, that system would need to understand how to validate that a particular learner’s eduID was truly associated with that learner, and they would need a mechanism for the learner to communicate the eduID string to the consumer out of band of delivering the badge, because Edubadges makes use of the `IdentityHash` option for protection of the user’s personal identifier in awarded badges.

Open Badges 3.0 introduces the possibility to use [Decentralized Identifiers (DIDs)](https://w3c.github.io/did-core/) to identify issuers and recipients of badges. This option appears in addition to other identifiers referenced by an OpenBadgeCredential. Previously, only one identifier, an email address, URL, or other `id` could be included in a badge, and now multiple identifiers may appear. The shift to OB 3.0 opens up the possibility to award badges that are issued to an that also record an email address for the user. This would help if a verifying consumer does not have the capability to prove that a certain learner holds a certain eduID.

Edubadges should aim for a flexible approach here. Keep the use cases that the identifier needs to be compatible with in mind:

*   As a learner, I can present my credential to another person, such as a hiring manager, so that this audience can verify the integrity of the signature, resolve the real-world organization that is the issuer, and determine that I am indeed the subject recipient.
*   As a learner, I can send my credential to my mobile wallet as a Verifiable Credential and then generate a Verifiable Presentation

Keep in mind the purposes of the learners who are intended to be the beneficiaries of the edubadges, as represented by this user story:

*   As a learner, I would like to present a badge to an educational institution or employer and have this consumer be capable of verifying that the badge belongs to me.

In order for the consumer to be able to validate this, the learner needs to be able to communicate what their recipient identifier is and needs to be able to communicate the badge. URL-based sharing will continue to be the leading mechanism by which badges are shared. Use cases will develop for direct verification of the Verifiable Credentials and the identifiers contained within them.

**Recommendation**: For an initial implementation phase where Open Badges are made accessible as file downloads, reference the learner’s eduID as `credentialSubject.identifier` where you express an `IdentityObject` (see [docs](https://1edtech.github.io/openbadges-specification/ob_v3p0.html#identityobject)) with an `identifierType` of `nationalIdNumber` or simply `identifier`, or `ext:eduID` as preferred. Hash the identifier as appropriate. Identify a mechanism by which learners can prove ownership of this credential when it is shared as a VC file for the pilot phase, and test the experience of several users who are instructed to share one of their badges like this in controlled conditions.

#### Issuer identifiers

Issuers may be identified either by HTTPS URLs or DIDs, but the question of what method to use for Edubadges issuers is not as simple as ensuring signing keys are appropriately reported in a DID document or issuer profile document resolved from the issuer identifier. Again, we must keep in mind how issuer information will be consumed to ensure that consumers have the ability not only to determine that credentials have been properly signed and have not been tampered with, but also that the issuer identifier truly corresponds to the real-world entity that is described in the credential.

If an issuer signs a credential using a `did:key` identifier, how does a consumer know whether the issuer name presented in a credential is trustworthy when the only thing they can verify automatically about the issuer is the association between the identifier and the credential signing key. That is an important capability, but trust in a credential also requires trust that the key is associated with an expected real-world institution, such as a University.

    {
        "issuer": {
            "id": "did:key:z6LStiZsmxiK4odS4Sb6JmdRFuJ6e1SYP157gtiCyJKfrYha",
            "type": "Profile",
            "name": "Example Corp",
            "url": "https://example.com/corp",
            "phone": "+1-222-333-4444",
            "description": "1EdTech University provides online degree programs."
        }
    }

This issue is not new to OB3, but OB3’s switch to signed verification brings it into focus. Even HTTPS identifiers for issuer profiles have the same problem, as these identifiers are typically URLs hosted by an issuing platform, rather than on an issuer’s actual registered domain name, but at least in these cases, consumers can trust the issuing platform does not allow unverified organizations to establish profiles. There needs to be some mechanism outside of the identifier itself that allows consumers to trust the integrity of the issuer metadata, for their purposes. This typically would involve delegation to some proxy responsible for registration of many profiles for a certain jurisdiction or market vertical, but the ecosystem of these “trust registries” remains immature. EBSI has begun work on a [Trusted Issuers Registry API](https://api-pilot.ebsi.eu/docs/apis/trusted-issuers-registry/latest#/), for example, but the scope is limited, likely only covering `did:ebsi` identifiers.

Identification of specific target consumers could enable clarification on what options may be practical for those consumers to obtain information about relevant issuers.

Besides `did:key`, `did:web` is the most commonly used DID method in early-stage OB3 implementations. `did:web` identifiers resolve to a HTTPS URL that hosts a document describing the entity. Using `did:web` could be a reasonable option to fall back to the Open Badges 2.0 style approach where the Edubadges domain name could be the main signal of trustworthiness for issued credentials, because target consumers for your credentials are likely to be aware of Edubadges and to understand that SURF only allows its institutional members to use the platform. This approach may not as easily cover other implementers of the edubadges open source code, because they may not have the reputational backing of an organization as trusted as SURF.

**Recommendation**: Use `did:web` identifiers that resolve back to a hosted URL on Edubadges (the existing backend, or a delegated microservice responsible for signing credentials, holding signing keys, and representing issuer profiles. See below about the possibility of using [ORCA](#orca---open-recognition-community-app) as such a microservice.)

#### Wallet integration

The Verifiable Credentials community is exploring how mobile wallets, often operating on mobile devices which cannot serve HTTP requests can receive credentials from issuers and communicate them to verifying parties. All Verifiable Credentials, including Open Badges can and will be communicated over a range of protocols. This is a space that is seeing significant experimentation pre-standardization.

Implementers have to cooperate to ensure high-quality user experience in the exchange of credentials between their products, both via OB and CLR APIs and emerging protocols to carry these credentials into next-generation use cases. When new user experience patterns are presented that aim to become universal, take care to help the user through the workflow, and give them fallback solutions whenever possible.

**Recommendations:** Implement wallet integration as a phase 2 pilot, after enabling basic signed credential download. Once Edubadges has identified wallet partners and is ready to invest in integration, the following recommendations apply to planning and executing this work, keeping in mind that the wallet ecosystem is early-stage:

*   Select specific integration partners who produce wallet software, and build solutions that work well with their software, while keeping aware of what aspects of the approach follow a particular standards-track protocol. In this early stage of ecosystem development, it is important to deliver a high quality user experience to learners, and there is no guarantee of compatibility with multiple different wallets with one implementation, because small differences in technology can produce dead ends for users.
*   Test integrations thoroughly, and communicate with your implementation partners to refine UX friction points for the benefit of users’ experience.
*   Share pain points in the broader credentials community (such as through 1EdTech or the Credentials Community Group) without exposing personal information, and learn about possible solutions from others.
*   Accurately inform users of the experimental status of features and integrations as necessary. Giving users an accurate sense of whether they are traveling a smooth and well-trodden path or a new route that may have pitfalls or dead ends goes a long way to gaining user trust.
*   Give users fallback options that are likely to succeed if the first path they try fails. For example, offer the chance to choose any wallet that uses a certain supported protocol, but suggest one particular integration as an easy choice, so users don’t get stuck if the wallet they previously used for a different issuer doesn’t work with the protocol used on your site. Sharing credentials by URL is good fallback choice to sharing VCs directly to a wallet, because learners can easily include URLs in a wide variety of communications to many different potential consumers.
*   Present benefits and risks to user to help them understand their choices. This example emphasized the user-owned nature of DIDs enabled by wallet connection in the face of the potential loss of control of an institutional or organizational email identifier. Products should make users aware of risks, such as any loss of data or verifiability that might be caused by losing a physical device.