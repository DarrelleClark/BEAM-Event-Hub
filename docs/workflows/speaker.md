# Speaker Workflow

## Purpose

Define speaker profile management, session assignments, materials, and attendee-facing speaker information.

## Speaker Access

Speaker access is granted through an approved role/invitation process. A speaker must not gain administrative access simply because they are assigned to a session.

## Profile

Speaker profiles contain approved public information such as:

- Name
- Photo
- Title/organization
- Biography
- Social/website links where approved

Sensitive internal fields must remain restricted.

## Session Assignments

1. Authorized event staff create/select a speaker.
2. Authorized staff select a session.
3. Create a `speakerAssignments` record connecting speaker and session.
4. Prevent duplicate active assignments.
5. Speaker can see sessions assigned to them.
6. Attendee-facing pages show approved speaker information for published sessions.

## Speaker Materials

Where enabled, speakers can upload or submit approved session materials. Storage paths and Firestore metadata must be scoped to the speaker/session and protected by backend rules.

## Speaker Dashboard

Recommended dashboard sections:

- Profile
- Assigned Sessions
- Session Details
- Materials
- Announcements
- Event information

## Editing Restrictions

Speakers may edit only fields explicitly permitted by the product design. They cannot modify their role, organization membership, session ownership, event publication state, or other administrative fields.

## Acceptance Criteria

- Speaker sees only authorized sessions.
- Duplicate assignments are prevented.
- Public profile fields are visible only when appropriate.
- Materials are protected by storage and database authorization.
- Speaker cannot escalate permissions through profile editing.
