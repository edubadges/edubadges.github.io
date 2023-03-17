### 7.4: Continued support for URL sharing and 2.0 verification.

Open Badges 3.0 can mean that badge sharing is more in the control of the learner, but discussions on this point typically ignore that many platforms, such as Edubadges, will need to continue offering URL-based sharing for badges. Anyone who has knowledge of a sharing URL can view some information about the achievement and its validity status, but Edubadges takes advantage of privacy features in Open Badges by only making OB 2.0 verification URLs accessible when learners have made badges public themselves, and by hashing recipient identifiers in badges.

While the ecosystem produces new and updated OB 3.0-compatible tools that obtain access to badges either from backpacks/hosts via the Open Badges API or through integration with Verifiable Credentials wallets of other types, 2.0 sharing and verification for existing clients will remain important. Think of the endpoints that support these features just as specific presentations or “serializations” of the underlying data, rather than as separate entities from the serializations of those same objects that support OB 3.0.

User stories that could guide preservation of these capabilities even as new 3.0 capabilities are added include:

*   As a learner who has earned an edubadge, I can access a signed OB 3.0 version of my badge whether or not I have marked the badge as public.
*   **No change**: If I mark my edubadge as public, I can copy a share URL that others can view.
*   **No change**: If I mark an edubadge as private after generating a share URL, when viewers attempt to access the share URL, no badge is returned.
*   **No change**: If a badge is marked as public, and a bot requests an HTML version of this page
*   **Enhancement**: If a client requests a frontend URL like `https://www.edubadges.nl/public/assertions/a41jSgmsSh6Sa1xcVUku5Q` and they request JSON as the response with `Accept: application/json` or `Accept: application/ld+json,application/json`, they should be 301 redirected to the backend URL `https://api.edubadges.nl/public/assertions/a41jSgmsSh6Sa1xcVUku5Q` for that object. This should apply to each the assertion, badgeclass/achievement, and issuer endpoints.

---

| [Back to Index](ob3-edubadges/README.md)   | [Previous Chapter 7: Appendix A: User Stories and Milestones](ob3-edubadges/70-appendix-a-user-stories-and-milestones.md)    | [Next Chapter 7.5: Share a badge to LinkedIn as a Certification on a user’s Profile](ob3-edubadges/75-share-a-badge-to-linkedin-as-a-certification-on-a-users-profile.md) |
| :--- | :---: | ---: |