Introduction
------------

SURF has contracted with Skybridge Skills to analyze how the Edubadges project could approach an upgrade from Open Badges 2.0 (OB2) to the forthcoming 3.0 version of the Open Badges Specification. The report will situate Open Badges 3.0 (OB3) implementation for the Edubadges project within a broader context of architectural needs and an evolving interoperability landscape within which awarded Edubadges are to have meaning.

This paper explores possible approaches to achieving OB3 implementation within the open source Edubadges system. The goal of this work will be to enable SURF’s Edubadges team to set and execute the 2023 product roadmap upgrading from Open Badges 2.0 to 3.0 alongside other product upgrades.

It will outline how to think about applying resources to enable pilot exploration of badges delivered as 3.0 and how the pilot phase can transition to a production service with minimal disruption for users of the existing Open Badges 2.0-based service.

A number of factors establish the landscape in which SURF aims to launch pilots and a production service offering Open Badges 3.0 capabilities. This paper addresses ecosystem components and trends including:

*   Open Badges 3.0 key features
*   The Verifiable Credentials Data Model
*   Spec development, release process, and conformance testing
*   Comprehensive Learner Record (CLR)

The Architecture Recommendations section lays out broad considerations that guide upgrading Edubadges into its next iteration that supports OB3:

*   Options for layers of the Verifiable Credentials tech stack.
*   User flows for privacy and control of personal data, updated for 3.0 capabilities, opportunities and challenges. Particularly, we consider how Edubadges can comply with a requirement to expunge personal data after 5 years without renewal of a user agreement that enables processing
*   Security considerations for custody of signing keys
*   Approaches to enabling consumer verification of badge awards for authenticity

Several use cases are explored in detail:

*   How to implement OB 3.0 at the data model level, with a discussion of the impact of the changes on how the “achievement” claimed by a badge may be understood
*   Data minimization and defensible deletion after retention period
*   Sharing badges to social media
*   SIS and LMS integration for badge award automation
*   How revocation works differently for cryptographically signed badges

The how-to section presents named development epics made up of user stories:

*   How to issue cryptographically signed Open Badges 3.0 `OpenBadgeCredentials` conformant with the 1EdTech specification
*   How to support sharing to social media or email via URL, supporting preview cards in platforms that use them
*   Approaches to achieving compatibility with standards and ecosystems relevant to Edubadges stakeholders, including Europass and the European Learning Model, EBSI, and eIDAS/ESSIF
