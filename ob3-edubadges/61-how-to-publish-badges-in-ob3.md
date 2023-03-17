### 6.1: How to publish badges in OB 3.0

Edubadges should think of implementing OB 3.0 as offering a serialization of a learner’s achievement, parallel to the OB 2.0 serializations already available. OB 2.0 were made available at the verification URLs for each Issuer, BadgeClass and Assertion. Sometimes the OB 3.0 data is available from endpoints like 2.0 is, and sometimes it is expressed as a downloaded OpenBadgeCredential data file.

See the [user stories](#enable-access-to-edubadges-in-ob-3.0-format) in the next chapter for how end users experience OB 3.0 in Edubadges.

The previous chapter laid out many of the choices involved with implementation of OB 3.0 and covered how the value of certain options may shift over time, depending on how the market develops. This section proposes a set of capabilities that would be a good choice for a pilot-scale implementation of OB 3.0 for Edubadges.

This section details each of the serializations involved in the implementation of OB 3.0, and how they compare to the versions of this data presented as OB 2.0 serializations.

**Note**: If Edubadges opts to adopt ORCA to manage OB 3.0 data, ORCA will manage all the responsibilities outlined in this section. ORCA is designed to implement the strategy represented here and expose API endpoints in VC-API format to enable Edubadges to store this data within ORCA as the institution’s copy held in their data pod.

#### OpenBadgeCredential (Assertion)

The following OB 2.0 assertion in Edubadges has some features to note:

*   A https URL is the `id`, where OB 2.0 `HostedBadge` verification is served.
*   A https URL is the `badge` identifier indicating which achievement (BadgeClass) this badge claims the learner had met the criteria of
*   The recipient identifier is the learner’s eduID, and `recipient.type` is `id`. This is a type that is not included in the list [recommended](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/index.html#ProfileIdentifierProperties) by Open Badges 2.0. When this approach was designed, it was imagined that the value hashed to represent the eduID here would be a URL, so the type of `id` (which maps in the OB 2.0 context to `@id`) is intended to serve much like a DID does in OB 3.0.

**OB 2.0 Assertion**:

    {
        "@context": "https://w3id.org/openbadges/v2",
        "type": "Assertion",
        "id": "https://api.edubadges.nl/public/assertions/a41jSgmsSh6Sa1xcVUku5Q",
        "badge": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g",
        "image": "https://api.edubadges.nl/public/assertions/a41jSgmsSh6Sa1xcVUku5Q/image",
        "verification": { "type": "HostedBadge" },
        "evidence": [],
        "issuedOn": "2022-12-05T14:21:04.517352+00:00",
        "recipient": {
            "hashed": true,
            "type": "id",
            "identity": "sha256$fe7d52dd605264c650461f79e5534b1714a8d13313cffcecce693b165be024d4",
            "salt": "b0aa39cc508e46bb8639ae1bad484a07"
        }
    }

The OB 3.0 serialization of this award is a signed OpenBadgeCredential. Make note of these characteristics:

*   The recipient identifier uses much the same mechanism as before, the eduID is hashed and included with a relevant type from the [identifier type enumeration](https://1edtech.github.io/openbadges-specification/ob_v3p0.html#identifiertypeenum-enumeration)
*   The Achievement uses the different `id` as the OB 2.0 assertion referenced as the `badge`. It is now embedded here in the OpenBadgeCredential rather than being linked by URL. It declares its relation to a 2.0 version of this achievement.
*   The issuer is identified using a `did:web` identifier that resolves via an HTTPS endpoint that returns a DID doc, as described below.
*   The issuer is redundantly embedded inside the Achievement as its `creator`. Now because Achievements can be issued by issuers other than their creator (though should not necessarily be trusted as equivalent by verifiers), this data appears twice in most cases where an achievement creator is defined. It is recommended to only express the required properties for the Profile embedded within an Achievement.
*   In OB 3.0, the type of this credential is `["VerifiableCredential", "OpenBadgeCredential"]`. The first entry comes from the Verifiable Credentials Data Model, and the second comes from OB 3.0. Within OB 3.0, `AchievementCredential` is a synonym of `OpenBadgeCredential` sometimes used by issuer systems upgrading from CLR 1.0, which was the origin of the more generic `Achievement` language.
*   This credential features an Edubadges URL as its `id`, which is the share URL for this award. It is recommended to explore whether there are use cases for retrieving OB 3.0 data from this endpoint, and the recommendation to use the same URL as the OB 2.0 assertion may change after pilot, if there is ever any use for retrieving this data from this endpoint.
*   A revocation list is linked for this credential. If this credential’s `id` appears in the list published at that URL, the credential should be considered revoked.
*   The Open Badges context URL `https://purl.imsglobal.org/spec/ob/v3p0/context.json` is expected to change to a `3.0.1` or similar version with the publication of the final spec, as 1EdTech is now avoiding making breaking changes without changing the context URL. Use the latest context available at implementation time, and keep the implementation updated to the latest context URL. Typically this will not require any changes to the JSON expression of OB 3.0 data.

**OB 3.0 OpenBadgeCredential**:

    {
        "@context": [
            "https://www.w3.org/2018/credentials/v1",
            "https://purl.imsglobal.org/spec/ob/v3p0/context.json",
            "https://w3id.org/security/suites/ed25519-2020/v1"
        ],
        "id": "https://api.edubadges.nl/public/assertions/a41jSgmsSh6Sa1xcVUku5Q",
        "type": ["VerifiableCredential", "OpenBadgeCredential"],
        "issuer": {
            "id": "did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg",
            "type": "Profile",
            "name": "SURF - Team edubadges",
            "url": "https://surf.nl/edubadges",
            "description": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
            "email": "support@edubadges.nl"
        },
        "issuanceDate": "2022-12-05T14:21:04.517352+00:00",
        "name": "Edubadge account complete",
        "credentialSubject": {
            "type": "AchievementSubject",
            "identifier": {
                "type": "IdentityObject",
                "hashed": true,
                "identityHash": "sha256$fe7d52dd605264c650461f79e5534b1714a8d13313cffcecce693b165be024d4",
                "identityType": "identifier",
                "salt": "b0aa39cc508e46bb8639ae1bad484a07"
            },
            "achievement": {
                "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g#v3p0",
                "type": "Achievement",
                "name": "Edubadge account complete",
                "description": "Welcome to edubadges. Let your life long learning begin! ###\r\n\r\nYou are now ready to collect all your edubadges in your backpack. In your backpack you can store and manage them safely. \r\n\r\nShare them anytime you like and with whom you like. \r\n\r\nEdubadges are visual representations of your knowledge, skills and competences.",
                "achievementType": "Achievement",
                "creator": {
                    "id": "did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg",
                    "type": "Profile",
                    "name": "SURF - Team edubadges",
                    "url": "https://surf.nl/edubadges",
                    "description": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
                    "email": "support@edubadges.nl"
                },
                "criteria": {
                    "narrative": "To qualify for this edubadge:\r\n* you successfully created an eduID,\r\n* you successfully linked your institution to your eduID,\r\n* you can store and manage them safely in your backpack."
                },
                "image": {
                    "id": "https://example.com//achievements/c3c1ea5b-9d6b-416d-ab7f-76da1df3e8d6/image",
                    "type": "Image"
                },
                "tag": [],
                "result": [
                    {
                        "type": "Result",
                        "id": "urn:uuid:",
                        "name": "This is an edubadge for demonstration purposes. The learning outcome for this edubadge is:\n* you have a basic understanding of edubadges,\n* you have a basic understanding how to use eduID."
                    }
                ],
                "related": [
                    {
                        "type": [
                            "Related",
                            "https://w3id.org/openbadges#BadgeClass"
                        ],
                        "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g",
                        "version": "Open Badges v2p0"
                    },
                    {
                        "type": ["Related"],
                        "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g/v3/nl",
                        "@language": "nl-NL"
                    }
                ]
            }
        },
        "proof": [
            {
                "type": "Ed25519Signature2020",
                "created": "2022-12-15T16:56:16Z",
                "verificationMethod": "did:example.com:issuers:540e388e-2735-4c3e-9709-80142801c774#key-0",
                "proofPurpose": "assertionMethod",
                "proofValue": "z4o2Pva6ksbXtCCzHv4VM8Ss9WJg2tnxgDbVwfZr1dq3i2jjzNHWPPpHHRw8s1AknGzL4XjBZVyh3BzSo59qz8NBp"
            }
        ],
        "credentialStatus": {
            "id": "https://api.edubadges.nl/issuers/lQ67BQQQS-eBx5syJGpazg/revocations/a169e",
            "type": "1EdTechRevocationList"
        }
    }

#### Achievement (BadgeClass)

In OB 2.0, the Achievement is identified by URL in the edubadge Assertion, and from that URL, a verifier may retrieve an Achievement like the example that follows, with these significant characteristics:

*   Uses the OB 2.0 context
*   Markdown is used in description, which is not a field that should allow markdown. It’s not invalid, but clients who display badges will not be likely to display formatting characters as plain text. Line breaks are typically respected for display.
*   Edubadges extensions are used to specify language and learning outcome.

**OB 2.0 BadgeClass**:

    {
        "@context": "https://w3id.org/openbadges/v2",
        "type": "BadgeClass",
        "name": "Edubadge account complete",
        "description": "### Welcome to edubadges. Let your life long learning begin! ###\r\n\r\nYou are now ready to collect all your edubadges in your backpack. In your backpack you can store and manage them safely. \r\n\r\nShare them anytime you like and with whom you like. \r\n\r\nEdubadges are visual representations of your knowledge, skills and competences.",
        "achievementType": "Achievement",
        "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g",
        "issuer": "https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg",
        "image": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g/image",
        "criteria": {
            "narrative": "To qualify for this edubadge:\r\n* you successfully created an eduID,\r\n* you successfully linked your institution to your eduID,\r\n* you can store and manage them safely in your backpack."
        },
        "alignment": [],
        "tags": [],
        "extensions:LanguageExtension": {
            "@context": "https://api.edubadges.nl/extensions/LanguageExtension/context.json",
            "type": ["Extension", "extensions:LanguageExtension"],
            "Language": "en_EN"
        },
        "extensions:LearningOutcomeExtension": {
            "@context": "https://api.edubadges.nl/extensions/LearningOutcomeExtension/context.json",
            "type": ["Extension", "extensions:LearningOutcomeExtension"],
            "LearningOutcome": "This is an edubadge for demonstration purposes. The learning outcome for this edubadge is:\n* you have a basic understanding of edubadges,\n* you have a basic understanding how to use eduID."
        }
    }

An example of how to publish an Achievement for OB 3.0 follows. Publishing Achievements on HTTPS `id`s is recommended for a wide variety of use cases, but some issuers will choose more ephemeral representations of their BadgeClasses, identifying them with `urn:uuid` randomly generated, non-resolvable identifiers.

The technical decisions here are consequential, but outcomes of how the ecosystem develops are hard to predict. See discussion below on [achievement definitions](#achievement-definitions-in-ob-3.0) and how they are expected to be handled within software that uses Open Badges.

Note also:

*   The `id` of the Achievement is not the same as that of the OB 2.0 BadgeClass, but the Achievement declares a “related” link back to the OB 2.0 version. The 2.0 version could be updated with a forward-looking link to the 3.0 representation.
*   The OB 2.0 type BadgeClass has been replaced by the more generic term Achievement for OB 3.0, but the concept remains the same.
*   The Open Badges 3.0 context updated term URLs for schema.org terms from `http` to `https`, and it is not practical to use both the OB 2.0 and OB 3.0 context files within one Badge.
*   Language can be expressed with `@language` and multiple translations provided with `related`.
*   The LearningOutcomeExtension is also no longer needed. You may use an instance of the Result class to express the outcome.

**OB 3.0 Achievement**:

    {
        "@context": "https://purl.imsglobal.org/spec/ob/v3p0/context.json",
        "type": ["Achievement", "https://w3id.org/openbadges#BadgeClass"],
        "@language": "en",
        "name": "Edubadge account complete",
        "description": "### Welcome to edubadges. Let your life long learning begin! ###\r\n\r\nYou are now ready to collect all your edubadges in your backpack. In your backpack you can store and manage them safely. \r\n\r\nShare them anytime you like and with whom you like. \r\n\r\nEdubadges are visual representations of your knowledge, skills and competences.",
        "achievementType": "Achievement",
        "creator": {
            "id": "did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg",
            "type": "Profile",
            "name": "SURF - Team edubadges",
            "url": "https://surf.nl/edubadges",
            "description": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
            "email": "support@edubadges.nl"
        },
        "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g",
        "issuer": "https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg",
        "image": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g/image",
        "criteria": {
            "narrative": "To qualify for this edubadge:\r\n* you successfully created an eduID,\r\n* you successfully linked your institution to your eduID,\r\n* you can store and manage them safely in your backpack."
        },
        "alignment": [],
        "tag": [],
        "result": [
            {
                "type": "Result",
                "id": "urn:uuid:",
                "name": "This is an edubadge for demonstration purposes. The learning outcome for this edubadge is:\n* you have a basic understanding of edubadges,\n* you have a basic understanding how to use eduID."
            }
        ],
        "related": [
            {
                "type": ["Related", "https://w3id.org/openbadges#BadgeClass"],
                "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g",
                "version": "Open Badges v2p0"
            },
            {
                "type": ["Related"],
                "id": "https://api.edubadges.nl/public/badges/EqLuTedxSEaQneSmWWlF4g/v3/nl",
                "@language": "nl-NL"
            }
        ]
    }

The achievement selected for the above example did not feature use of Alignment. Alignment changed slightly for OB 3.0:

*   Ensure at implementation time that the type alias `Alignment` remains correct for the spec. See this [issue](https://github.com/1EdTech/openbadges-specification/issues/502). `"type": "Alignment"` is now required in this object.
*   A new `targetType` field is added with a range of [possible values](https://1edtech.github.io/openbadges-specification/ob_v3p0.html#org.1edtech.ob.v3p0.alignmenttargettype.class).

**Example of Alignment in OB 3.0 Achievement**:

    {
        "type": "Achievement",
        "alignment": [
            {
                "type": "Alignment",
                "targetName": "Strengthen Relationships",
                "targetUrl": "https://credentialfinder.org/competency/ce-bc81d5de-6356-4ffd-a93f-4b13bc851882",
                "targetDescription": "Individuals who can strengthen relationships add value in the 21st century workplace by creating networks through which they access and provide resources, information, and support.",
                "targetFramework": "Education Design Lab 21st Century Skills",
                "targetCode": "ce-bc81d5de-6356-4ffd-a93f-4b13bc851882",
                "targetType": "ceasn:Competency"
            }
        ]
    }

#### Issuer Profile

In Edubadges’ OB 2.0 implementation, an issuer record shown below has these characteristics:

*   It includes all the required properties for OB 2.0 and some additional data not included in the core spec. This additional data appears either as extensions or as extra properties for translations that don’t match term definitions in the context and would be dropped upon JSON-LD operations. This data is only intended to be consumed by the Edubadges system itself.

**OB 2.0 issuer Profile**:

    {
        "@context": "https://w3id.org/openbadges/v2",
        "type": "Issuer",
        "name": "SURF - Team edubadges",
        "name_english": "SURF - Team edubadges",
        "name_dutch": null,
        "url": "https://surf.nl/edubadges",
        "url_english": "https://surf.nl/edubadges",
        "url_dutch": null,
        "email": "support@edubadges.nl",
        "description": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
        "description_english": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
        "description_dutch": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
        "id": "https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg",
        "image": "https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg/image",
        "image_english": "https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg/image?lang=en",
        "extensions:InstitutionIdentifierExtension": {
            "@context": "https://api.edubadges.nl/extensions/InstitutionIdentifierExtension/context.json",
            "type": ["Extension", "extensions:InstitutionIdentifierExtension"],
            "InstitutionIdentifier": "0000"
        },
        "extensions:GradingTableExtension": {
            "@context": "https://api.edubadges.nl/extensions/GradingTableExtension/context.json",
            "type": ["Extension", "extensions:GradingTableExtension"],
            "GradingTableURL": "https://www.surf.nl/"
        },
        "extensions:InstitutionNameExtension": {
            "@context": "https://api.edubadges.nl/extensions/InstitutionNameExtension/context.json",
            "type": ["Extension", "extensions:InstitutionNameExtension"],
            "InstitutionName": "SURF"
        }
    }

An updated representation in OB 3.0 has a few features to note:

*   This is a DID Document that is returned for an HTTP request made to a URL on the Edubadges system.
*   The OB 3.0 type for this document is renamed “Profile” from the OB 2.0 “Issuer”. OB 2.0 registered “Profile” as an alias of “Issuer”.
*   It contains a public key representation of an EdDSA curve key. The key has an `id` that includes the issuer id and a fragment identifier `#key-0`.
*   The institutional identifier can now be expressed as an “otherIdentifier”, as can the OB 2.0 URL as a `sourcedId` (a weak recommendation, subject to change).

**OB 3.0 issuer DID Document**:

    {
        "@context": [
            "https://www.w3.org/ns/did/v1",
            "https://www.w3.org/2018/credentials/v1",
            "https://purl.imsglobal.org/spec/ob/v3p0/context.json",
            "https://w3id.org/security/suites/ed25519-2020/v1"
        ],
        "id": "did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg",
        "type": "Profile",
        "name": "SURF - Team edubadges",
        "url": "https://surf.nl/edubadges",
        "description": "Edubadges is an infrastructure developed by SURF. Dutch educational institutions can use it to award digital certificates to their students or staff.",
        "email": "support@edubadges.nl",
        "otherIdentifier": [
            {
                "type": ["IdentifierEntry"],
                "identifierType": "sourcedId",
                "identifier": "https://api.edubadges.nl/public/issuers/lQ67BQQQS-eBx5syJGpazg"
            },
            {
                "type": ["IdentifierEntry"],
                "identifierType": "identifier",
                "identifier": "0000"
            }
        ],
        "verificationMethod": [
            {
                "id": "did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg#key-0",
                "type": "Ed25519VerificationKey2020",
                "controller": "https://example.com/issuer/123",
                "publicKeyMultibase": "z6Mkf5rGMoatrSj1f4CyvuHBeXJELe9RPdzo2PKGNCKVtZxP"
            }
        ]
    }

#### Revocation List

Edubadges uses OB 2.0 `HostedBadge` verification, which means each edubadge functions as its own revocation endpoint. In addition, any edubadges marked private return `404` status and are considered invalid. See details on [revocation](#revocation) below.

OB 3.0 relies on portable signed credentials, so issuer publishes a revocation list. Here is a sample implementation of 1EdTech’s Revocation List Status Method.

**Status list reference in OpenBadgeCredential**:

    {
        "credentialStatus": {
            "id": "https://api.edubadges.nl/issuers/lQ67BQQQS-eBx5syJGpazg/revocations/a169e",
            "type": "1EdTechRevocationList"
        }
    }

The ID above responds with a revocation list. Notes about this response:

*   The `id` of this list may be a partial representation of revocations by this issuer. It may contain fake data.
*   The 1EdTech Revocation List spec doesn’t specify a `@context`, but it is recommended that Open Badges implementers use the Open Badges context. The necessary terms `revokedCredentials` and `revocationReason` will be added to the Open Badges context before its release.

**Revocation List Response**:

    {
        "@context": "https://purl.imsglobal.org/spec/ob/v3p0/context.json",
        "id": "https://api.edubadges.nl/issuers/lQ67BQQQS-eBx5syJGpazg/revocations/a169e",
        "issuer": "did:web:api.edubadges.nl:issuers:lQ67BQQQS-eBx5syJGpazg",
        "revokedCredentials": [
            {
                "id": "http://example.edu/credentials/3732",
                "revoked": "true",
                "revocationReason": "No final payment"
            }
        ]
    }

---

| [Back to Index](ob3-edubadges/README.md)   | [Back to Chapter 6: Use Cases in Detail](ob3-edubadges/60-use-cases-in-detail.md) |    [Next Chapter 6.2: Achievement definitions in OB 3.0](ob3-edubadges/62-achievement-definitions-in-ob3.md) |
| :--- |  :---:  | ---: |