# Sessions Collection

## Overview

The `sessions` collection stores every scheduled activity within an event.

A session represents any attendee-facing activity such as a keynote, breakout session, workshop, panel discussion, networking event, training, ceremony, competition, or virtual presentation.

Each session belongs to one event, one venue, one room, and one track.

Speakers are **not stored directly** in the session document. Instead, they are linked through the `speakerAssignments` collection, allowing one session to have multiple speakers and one speaker to present multiple sessions.

---

# Firestore Collection

sessions

---

# Purpose

The Sessions collection powers the core attendee experience.

It is used by:

- Home Dashboard
- Schedule
- Session Details
- Speaker Profiles
- QR Pass
- Notifications
- Check-In
- Reports
- Analytics

---

# Document ID Strategy

Firestore Auto ID

Example

session_01

---

# Session Types

Supported values

- Keynote
- Breakout
- Workshop
- Panel Discussion
- Fireside Chat
- Networking
- Roundtable
- Training
- Competition
- Ceremony
- Lunch
- Break
- Expo
- Virtual Session

---

# Session Status

Supported values

- Draft
- Published
- In Progress
- Completed
- Cancelled
- Archived

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |
| venueRef | Document Reference | Yes | Venue |
| roomRef | Document Reference | Yes | Room |
| trackRef | Document Reference | Yes | Track |

---

## Basic Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| sessionTitle | String | Yes | Session title |
| shortTitle | String | No | Short title |
| description | String | Yes | Full description |
| sessionType | String | Yes | Session category |
| imageUrl | String | No | Banner image |
| featured | Boolean | Yes | Featured session |

---

## Schedule

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| startTime | Timestamp | Yes | Session start |
| endTime | Timestamp | Yes | Session end |
| durationMinutes | Number | Yes | Duration in minutes |

---

## Registration

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| capacity | Number | No | Maximum attendees |
| waitlistEnabled | Boolean | Yes | Enable waitlist |
| requiresRegistration | Boolean | Yes | Registration required |
| allowWalkIns | Boolean | Yes | Walk-ins allowed |

---

## Virtual Resources

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| livestreamUrl | String | No | Livestream link |
| recordingUrl | String | No | Recording link |
| presentationUrl | String | No | Presentation slides |

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| tags | List<String> | No | Search keywords |
| status | String | Yes | Session lifecycle |
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Creation date |
| updatedBy | Document Reference | No | Last editor |
| updatedAt | Timestamp | Yes | Last update |

---

# Relationships

```
Organization
      │
      ▼
Events
      │
      ▼
Sessions
      │
      ├── SpeakerAssignments
      ├── Registrations (Future)
      ├── Favorites (Future)
      ├── Attendance (Future)
      ├── Feedback (Future)
      └── Notifications (Future)
```

---

# Business Rules

- Every session belongs to one organization.
- Every session belongs to one event.
- Every session belongs to one venue.
- Every session belongs to one room.
- Every session belongs to one track.
- Sessions may have multiple speakers.
- Speakers may present multiple sessions.
- Start time must occur before end time.
- Session duration must be greater than zero.
- Capacity cannot be negative.
- Cancelled sessions remain visible.
- Archived sessions cannot be modified.

---

# Validation Rules

Required

- organizationRef
- eventRef
- venueRef
- roomRef
- trackRef
- sessionTitle
- description
- sessionType
- startTime
- endTime

Validation

- End time must be after start time.
- Duration must be greater than zero.
- Capacity cannot be negative.

---

# Security Rules

## Read

Published sessions

Authenticated users

Organization Staff

Super Admin

---

## Create

Organization Admin

Event Manager

Super Admin

---

## Update

Organization Admin

Event Manager

Assigned Speaker (limited fields only)

Super Admin

---

## Delete

Super Admin

Recommendation

Archive instead of deleting.

---

# Firestore Queries

## Sessions by Event

eventRef == selectedEvent

---

## Sessions by Track

trackRef == selectedTrack

---

## Sessions by Room

roomRef == selectedRoom

---

## Upcoming Sessions

startTime > currentTimestamp

status == "Published"

---

## Featured Sessions

featured == true

---

## Search Sessions

Search

- sessionTitle
- description
- tags

---

# Composite Indexes

organizationRef ASC

eventRef ASC

startTime ASC

---

trackRef ASC

startTime ASC

---

roomRef ASC

startTime ASC

---

status ASC

startTime ASC

---

featured ASC

startTime ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| Read | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Update | ❌ | Assigned Session Only | ❌ | ✅ | ✅ | ✅ |
| Delete | ❌ | ❌ | ❌ | ❌ | Archive | ✅ |

---

# Used By

- Home
- Schedule
- Session Details
- Speaker Profile
- QR Pass
- Notifications
- Reports
- Admin Dashboard
- Volunteer Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "venueRef": "/venues/venue_01",
  "roomRef": "/rooms/room_01",
  "trackRef": "/tracks/track_01",
  "sessionTitle": "Leading with Purpose",
  "shortTitle": "Leadership Keynote",
  "description": "A keynote focused on leadership development and community impact.",
  "sessionType": "Keynote",
  "imageUrl": "",
  "featured": true,
  "startTime": "2027-03-20T09:00:00Z",
  "endTime": "2027-03-20T10:30:00Z",
  "durationMinutes": 90,
  "capacity": 500,
  "waitlistEnabled": true,
  "requiresRegistration": true,
  "allowWalkIns": false,
  "livestreamUrl": "",
  "recordingUrl": "",
  "presentationUrl": "",
  "tags": [
    "Leadership",
    "Education",
    "Community"
  ],
  "status": "Published",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- AI-powered session recommendations
- Live Q&A
- Polling
- Session chat
- Digital certificates
- Continuing education credits
- Session ratings
- Session attendance analytics
- AI-generated summaries
- Calendar synchronization
