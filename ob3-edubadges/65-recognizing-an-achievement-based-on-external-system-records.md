### 6.5: Recognizing an achievement based on external system records

Open Badges can recognize a wide variety of achievements, but the scalability of the processes by which they come to be issued is a more important factor than the breadth of our imaginations when it comes to predicting which badges will actually find their ways to learners’ backpacks. The process of issuing badges to a large population of learners smoothly during the course of their engagement with an institution often means identifying the systems where authoritative data is already kept about the achievements that matter within that institution and processing it to respond to newly tracked achievements that should result in badges.

Student Information Systems (SIS) are often the best authoritative data repository institutions hold for student achievements rising to the level of the official transcript, and Learning Management Systems (LMS) are often the best source of data about course-level assessments and outcomes. Gradually, more institutions are reporting an expanded array of learning outcomes up to the systems at the SIS and registrar level, increasing the possibilities that they can be recognized with Open Badges or included in diplomas and other official documents, digital or otherwise.

API integration between Edubadges and SIS or LMS systems can enable credential issuing processes to reach the scale of whole student populations. Here is a general outline of how Edubadges can approach this challenge:

*   Understand that the function of a SIS or LMS is to store and represent the current state of learner enrollments and educational achievements. At any given time, the information available from such a system could appear as a set of facts or attributes about many users. The purpose of the assembly of these facts is primarily to enable management and tracking of the learning that students are currently doing. Secondary purposes for the data involve aggregate reporting or making it available to other systems.
*   The Edubadges system also serves as a registry of facts with some overlapping scope, but the focus of its registry is future-looking, enabling verification from external systems of meaningful achievements that occurred during a student’s education journey in a SURF member institution.
*   Each badge award should be understood as an issuer’s claim that a particular learner has met the criteria of a particular achievement as of a particular date. The Edubadges system keeps track of which criteria have been met by which users (the earners of a badge) and makes it possible for those earners to obtain a signed copy of the credential making this claim at any time, on-demand. The availability of the badge is a capability Edubadges offers related to the continued existence of a set of facts held in that issuer’s systems that qualify the claim but it is not a replacement for the existence of the underlying data or an automatic consequence of that data being stored in the SIS or LMS.
*   SIS or LMS data changes in response to events, such as enrollments confirmed in a scheduling system or grades entered into an assessment system.
*   The change in SIS or LMS data that occurs when a learner goes from not meeting the criteria for a badge to meeting that criteria can be detected by Edubadges as it processes potentially qualifying events through analyzing various facets of the data over time.
*   Edubadges needs to respond to a change in SIS or LMS data as if it is responding to an event, but as data is often stored and made accessible in terms of the resultant data rather than the raw event data, Edubadges may need to process large amounts of data in order to identify whether or not badges need to be awarded (or revoked) across a set of students. For example, if awarding a badge is desired for students who have completed a course, Edubadges would need to respond to events including the enrollment of a student in the course, the entry of a final grade or result for a student, the unenrollment of a student, or the change in a grade or result for a student. Processing whether a qualifying event occurred might look like
*   Sometimes “event stream” data from a SIS or LMS is available for processing by a system like Edubadges. This can appear to be a simpler problem to solve than the above state-comparison work, but there are challenges here as well. Filtering events that appear in the stream for qualifying events meeting a certain badge criterion, or ensuring that no events are skipped or lost in transmission are often difficult to accomplish at scale. Event stream systems are sensitive to performance issues. Sometimes, use cases may require the combination of multiple events to result in one badged outcome, and tracking the state of partially completed criteria is difficult.
*   Sometimes it is possible, through partnership or another means of coordination, to build badge trigger business logic directly into a SIS or LMS system. This may enable event triggers to be placed “closer” to the contexts in which all the relevant data surrounding why the event might qualify a learner for a badge may be readily available. In this scenario, the SIS or LMS now needs to understand which badges might be available for a user to assign to actionable criteria and how to trigger the right badge award via Edubadges’ API when a qualifying event or set of events occurs.
*   The lifespan of data tracked in the underlying SIS or LMS system, that stored in the credential system, and that held only by the user themselves, may differ from one another. For example, some months after a student graduates, their submitted assignments and the individual grades on those assignments, as well as the entire records of the specific session of a course they took, might be expunged from the LMS, while the SIS still holds records of which courses that student had completed. The credentials system, Edubadges, might hold associated awarded credentials for several years after the student graduates (see [data minimization](#data-minimization-and-defensible-deletion-after-retention-period)). And the student might hold in a mobile wallet their exported signed edubadges, each of which remain valid even after Edubadges removed personally identifiable data from the version of those badges in its database.

The complexity of the task of tracking events from aggregate state data, such as is usually available from an SIS or LMS is large. Any investment in integration that covers the automation of badge awards or of student roster synchronization is large and should be assumed to occupy months of development effort for a well-staffed team. If there are opportunities for the business logic and user interfaces to be placed into the SIS or LMS instead of into Edubadges, this can potentially result in massive reductions of complexity, but these options are some times not possible because these products are often made by other vendors.