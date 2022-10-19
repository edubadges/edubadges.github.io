# Edubadges Architecture
    
There are 3 main components that form the Edubadges service:
- The backend server or API-server
- The frontend server or UI-server
- The validator service

### Edubadges backend
See https://github.com/edubadges/edubadges-server

This is a Django / Python3 application which provides the APIs to the various other applications.
This backend is only accessible by the administrators and only possible via MFA and uname/pwd. 
The backend application displays the Django Staff Dashboard with which the application and data can be managed.
    
### Edubadges frontend
See https://github.com/edubadges/edubadges-ui

This provides access for both students (edubadge recipients) and teachers (Edubadge issuers).
Students log in via eduID on the edubadges backpack and lecturers log in via SURFconext on the issuer portal.
Depending on which login is followed and which rights the user has, the frontend application offers different functionalities:
Students log in via eduID and see their backpack. This is where students can apply for edu badges and waa their earned edu badges are stored.
Here they can also create collections; these are collections of edu badges, see which applications they have made and manage their account. 
Teachers log in via SURFconext and can have the following roles:

- Institution Admin
- Issuer Group Admin
- Issuer Admin
- BadgeClass Admin, BadgeClass Editor, BadgeClass Issuer

Depending on these rights, teachers can create issuers, create badge classes, issue badges and perform account management tasks.

### Edubadges validator
See: https://github.com/edubadges/edubadges-validator

This is a separate Python3 service that is provided to validate edubadges and has an API that allows publicly milled edubadges to be validated.
This is an open service that can be used by anyone. One can upload an edubadge PNG image or enter the edubadge assertion URL or JSON data or JWS data to check the validity of an edubadge and to see an edubadge's metadata.
