### 3.5: Verifiable Credentials wallets

The largest unknowns for Edubadges are around wallets. Initiatives are spinning up with a dizzying array of variety, and integration with one wallet does not guarantee compatibility with another, even within the same family of wallets. For example, the recent [JFF Plugfest](https://w3c-ccg.github.io/vc-ed/plugfest-2-2022/) featured around 20 implementers across three different families of VC wallet protocols. All the demonstrations were about very similar Open Badges, but not all products were compatible with one another.

SURF does not expect to build a credentials wallet. The scope of such an undertaking would be too large. Simply maintaining compatibility over time with mobile operating systems would require frequent but unpredictable workloads. Even if SURF were to invest in building a wallet, it is not clear that OB 3.0 would be the main target for credentials schema. The European Digital Identity wallet ecosystem based on eIDAS toolkit requirements are complex – 80 pages, supporting a potentially large range of different protocols and credential schemas.s

Just like how value for Edubadges is dictated by the credential destinations that the service can connect with, wallet apps get their value from issuers and “verifiers” they connect with. While the vast majority of initiatives mentioned in this report are compatible with Verifiable Credentials, there are many different options that govern whether two products are interoperable in practice. Among these is the protocol over which an issuer or verifier service connects to a wallet, receives identity and authentication information from the wallet and then communicates credentials. There are several such protocols in development.

Protocols under development to transport Verifiable Credentials including Open Badges and CLR include:

*   [Credential Handler API (CHAPI)](https://w3c-ccg.github.io/credential-handler-api/)
*   [DIDComm](https://identity.foundation/didcomm-messaging/spec/v2.0/)
*   [OIDC4VCI](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)

What does it look like from a user’s perspective to interact with a mobile wallet? This example uses a general representation of workflow for multi-device integration similar to what occurs in all of the above protocols. The different protocols vary in UX slightly, and they use different steps “under the hood” in between user actions.

> Pieter is signed into Edubadges, looking at the achievements he has earned. He sees these credentials are associated with his eduID. He can make each badge publish to share by URL if he wishes, but Pieter also sees another option to connect a wallet on his mobile device, where he can use a securely generated passkey to create a cryptographically verifiable Decentralized Identifier (DID) to use. Links appears to mobile app stores for a mobile wallet that supports integration with Edubadges.
> 
> Pieter installs the app on his phone and sets it up. Back in Edubadges on his desktop computer browser, he selects to proceed to connect to a mobile wallet. He chooses edubadges representing courses and several of the competency achievements to send to the wallet initially. He is directed to an experience where he is directed to scan a QR code displayed on screen. The scan results in a URL that he can open in the wallet app he installed. He sees a confirmation screen where his wallet asks if he would like to confirm a connection to Edubadges. He approves this request and is informed that there is a successful connection. He looks back at his desktop browser and sees a confirmation screen there as well saying that credentials have been downloaded to the wallet. On the phone in the list of credentials he sees the edubadges he selected to send.

Here, Pieter walks through the experience of downloading a mobile app to use as a wallet for credentials including several `OpenBadgeCredential`s. Edubadges is compatible with one particular wallet that was chosen for a pilot here, though in the future, the service might support integration with other wallets as well, that might use different options for the various layers of the credentials tech stack.


---

| [Back to Index](ob3-edubadges/README.md)   | [Back to Chapter 3: The Open Badges and Digital Credentials Landscape](ob3-edubadges/30-the-open-badges-and-digital-credentials-landscape.md) |    [Next Chapter 3.2: 1EdTech specification process](ob3-edubadges/32-1edtech-specification-process.md) |
| :--- |  :---:  | ---: |