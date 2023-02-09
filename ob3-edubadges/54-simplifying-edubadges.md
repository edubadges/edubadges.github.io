### 5.4: Simplifying Edubadges

Edubadges-server is a python application using the Django web application framework. This technology is not SURF’s preferred tech stack, though it is a common framework, and it is easy enough to employ developers with relevant experience who can make modifications. There is some support for responsibly migrating away from the use of this system component, slowly replacing it with a newer service that is more tailored to the core workflows of the application.

Rewriting this integral piece of the system for a future release from scratch, while continuing to maintain and support a production service based on the edubadges-server Django backend is almost certainly an over-ambitious strategy. It is unlikely that sufficient budget could be dedicated to a complete re-write of existing functionality. The number of intricately interwoven workflows represented in the `edubadges-server` code is high, and test coverage of the API is not thorough enough to be confident that tests could detect broken functionality or identical performance of a replacement.

The practical path forward is not simple, but it prioritizes working software at every release. A three phase approach is called for:

1.  Simplification of the existing edubadges-server system and improvements to test coverage
2.  Integration of intentionally scoped replacement components for core OB3 workflows
3.  Expansion of replacement components to cover all necessary functionality of edubadges-server

Edubadges carries a lot of the weight of its development history, such as workflows specific to how Concentric Sky used its parent open source project badgr-server. On top of its early architecture, years of improvements, new features, and dependency upgrades have been added, and as is common with many projects, features have often not been removed when they are no longer needed. The continued maintenance of more features than the software truly needs to serve will stand in the way of efficient future development. It is therefore important that as the new OB3 features are added, that they are not just stacked on top of existing features where they fit. Some existing features must be removed in order to make it possible to open up seams for the integration of new features or architectural components.

**Recommendation**: Features that should be considered for removal:

*   BadgrApp & Theming support in backend (Consider moving necessary theme config to edubadges-ui)
*   Open Badges 1.1 JSON rendering support.
*   “Original JSON” data mixing into presentation of badge data
*   As many model mix-ins as possible that are referenced in `issuer.models`
*   `badgrlog` Django app (unless you are actively using the data produced by this verbose logging system)
*   `health` Django app (unless you are actively using this endpoint for health checking)
*   `notifications` Django app (Notifications of endorsement could be removed so that they could be rebuilt as needed)
*   `composition` Django app (remove dependencies to migrations referenced in other apps)
*   `signing` Django app (remove ability to sign badges using a 2.0-style strategy)

Features that should be improved or overhauled:

*   Untangle use of CacheModel (Missed timely cache population is a frequent source of bugs)
*   Replace `allauth` dependency with new more maintainable custom code for auth. This part of the code is intricate and where security risks may crop up. It is very difficult to debug parts of the eduID integration because of the allauth dependency. Search for a new library or rewrite with your own code based on underlying SAML or OAuth/OIDC libraries compatible with Django 5.0, which will have some backwards-incompatible changes. See [release plan notes](https://django.readthedocs.io/en/latest/releases/5.0.html#backwards-incompatible-5-0).

Test coverage improvement is not necessarily a fun activity, but it both improves developer familiarity with the system and improves the ability to be confident that feature removals and modifications have not disrupted critical workflows. Thorough manual QA will also be important to ensure simplified components connected to features that were removed continue to function as designed.