# Attendee Workflow

## Purpose

Define the attendee experience from sign-in through event discovery, schedule planning, session details, speaker discovery, registration, QR pass, announcements, and profile management.

## Home

The Attendee Home loads the current/published event context, featured sessions, announcements, sponsor content where configured, and quick actions such as Schedule and QR Pass.

## Event Discovery

Attendees can view published events that they are permitted to access. Draft, archived, private, or otherwise restricted events must not appear through public attendee queries.

## Schedule

1. Load sessions for the selected/current event.
2. Filter by day, track, room, or other supported filters.
3. Open Session Details.
4. Display title, description, time, room, track, and assigned speakers.
5. Support adding/removing sessions from the attendee's personal schedule where that feature is enabled.

## Session Details

Session details should include:

- Title
- Description
- Start/end time
- Room/location
- Track
- Speakers
- Relevant materials/links when authorized

## Speaker Directory

Attendees can browse speakers associated with published sessions. Speaker profiles should expose only approved public profile fields.

## Registration

From an eligible event, the attendee selects Register. The registration workflow handles duplicate prevention, registration status, and ticket/pass creation.

## QR Pass

The attendee can open their active event pass. The pass should show the approved event/ticket information and a QR identifier without exposing unnecessary personal information.

## Announcements

Attendees see published announcements for events/organizations they are authorized to access. Draft and targeted announcements must not leak through queries.

## Profile

Attendees can view/update permitted profile fields, notification preferences, timezone/language preferences, and other approved settings. Email identity and role-controlled fields should not be editable through ordinary profile actions unless explicitly authorized.

## Navigation

Primary attendee navigation:

Home → Schedule → Session Details → Speaker Profile → QR Pass → Notifications → Profile.

## Error and Empty States

Every attendee page must define loading, empty, permission-denied, offline/network-error, and generic retry states where applicable.

## Acceptance Criteria

- Attendee sees only published/authorized events.
- Schedule queries are scoped to the selected event.
- Session and speaker navigation works.
- Registration cannot create duplicates.
- QR Pass only exposes the attendee's authorized pass.
- Profile updates do not allow role or permission escalation.
