### 6.4: Sharing badges to social media

With the move from hosted verification to signed credentials, issuer platforms like Edubadges no longer have a responsibility to host a representation of badge award data publicly available for verification at a specific URL. But consumer-side applications that receive credential data in VC/OB3 format are not yet prevalent, so Edubadges needs to continue to build software for the

How to support sharing to social media or email via URL, supporting preview cards in platforms that use them.

> Gene receives an Open Badge for the completion of a certificate program and wants to include it verifiably on a professional social network. He can post a reference to the badge as a URL on the his profile. The social network site displays a summary card showing the credential information.

The URL is the universal mechanism for sharing content on the web. URLs provide the easiest mechanism for badge recipients to share their achievements on social media, in resumes, and job applications. The vast majority of last-generation Open Badges 2.0 and CLR 1.0 credentials in production support URLs for both verification and sharing. Learners’ need to be able to place their achievements verifiably into platforms via URL sharing will continue, but platforms that hold their data are encouraged to take advantage of new OB 3.0 and CLR 2.0 capabilities to grant greater control over sharing to data subjects themselves as they implement share by URL capabilities.

Recommendations for the use of share URLs include:

*   Give data subjects easy to use options to limit or grant access to data or inclusion of their data in directories. Do not publish learner achievement data in credential format on unauthenticated URLs by default.
*   If Open Badges 2.0 verification endpoints are used, use content negotiation on sharing URLs to enable the presentation of Use [Open Graph Protocol](https://ogp.me) tags on the sharing URLs to enable easy generation of card previews.

**Will social media platforms, job boards, and other websites where lifelong learners leverage their experience to discover and unlock new opportunities support OB3?**

The need to share badges by URL exists because these platforms do not yet support direct examination and verification of the Open Badges and Verifiable Credentials themselves. LinkedIn, job boards, and HR standards organizations and members are aware of OB3 and VC, but they are not stepping forward to be early stage large scale consumers of these records. This is a typical conservative position that one [often sees](https://en.wikipedia.org/wiki/The_Innovator's_Dilemma) in incumbent market leading companies, where they cannot spend time adopting experimental technologies because they are too busy responding to customer and business needs. It is not an indication that these platforms will not adopt digital credentials, it’s just a sign that the credentials are not yet perceived to be a significant source of value. Once the killer apps develop, and easy to use implementation patterns for credentials that offer access to pools of credentials of known value, more platforms will begin to offer credential import experiences that open up real resources and opportunities to users within their platforms.

#### Sharing to LinkedIn as a Certification on the Profile

One specific sharing scenario that will remain important to learners is the ability to share to the professional social network LinkedIn. [User stories](#share-a-badge-to-linkedin-as-a-certification-on-a-users-profile) for this type of sharing are presented later in this report. LinkedIn features a news feed of timely posts and a profile, where professionals save information about their skills, work experience, and certifications. It is possible to add a “Certification” that is verifiable by URL to this section of the profile, where it remains visible to anybody who is looking at the learner’s qualifications there, unlike the news feed posts which slide into obscurity over time, hidden by newer posts in the “Activity” section.

LinkedIn doesn’t follow the Open Badges model for credentials, but most of the fields in its Certification model align to parallel fields within an `OpenBadgeCredential` or `Achievement`. The biggest difference to be aware of is around the image shown within LinkedIn. There is no field to identify a badge image per certification, but if an issuer is identified among organizations that have established a [LinkedIn Page](https://business.linkedin.com/marketing-solutions/linkedin-pages), the issuer’s profile picture/logo uploaded to that LinkedIn Page is shown on the learner’s profile.

Here is an example of a URL that opens an Add to Page form. LinkedIn has detailed [documentation](https://addtoprofile.linkedin.com/) about the ability to pre-fill the form, centering on the ability to generate a URL that uses query parameters attached to relevant fields. Each parameter’s value is url-encoded.

    https://www.linkedin.com/profile/add/
    ?startTask=CERTIFICATION_NAME
    &name=Nice%20Working%20With%20You
    &organizationId=15183410
    &issueYear=2021
    &issueMonth=10
    &certUrl=https%3A%2F%2Fapi.badgr.io%2Fpublic%2Fassertions%2FO4jOj-yoQUy0geapsoQUug&certId=617c2c46fc482245298e9c16

Most of these parameters are straightforward. There is one significant exception, in that that `organizationId` or `organizationName` is required. This refers to the ID number of a specific page on LinkedIn that is shown as the issuer of the certification. Issuers that have a registered page on LinkedIn are shown with an improved interface including a link to that page. The difficulty is that the discovery of the ID to use for this parameter is difficult. One option is to integrate with the LinkedIn API and try to search for organizations, but this makes a sharing feature much more complex to implement. Users can obtain this information themselves if they are an admin for the organization by copying it from the URL bar while in the management interface for their LinkedIn page, but this may confuse users who are asked to associate the issuer. The fallback option `organizationName` is easiest to use. Start with that as the issuer name, and then if staff members of the issuer of a badge are capable of identifying their organization page URL with the `organizationId` number in it, a more complex workflow for editing the issuer to add that information may be implemented. Another digital credentials product, Accredible, has a [help page](https://help.accredible.com/how-do-i-find-my-linkedin-organization-id) that shows a user where to find this information, further evidence that the concept of `organizationId` is not well known to LinkedIn users.

Generate a URL by populating the parameters `name`, `organizationName`, `issueYear`, `issueMonth` and `certUrl` in a new window when a user selects the share to LinkedIn profile option. The new window can be small in size on desktop environments.