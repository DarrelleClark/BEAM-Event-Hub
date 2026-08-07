# Speaker Assignments Collection

## Overview

The `speakerAssignments` collection creates the relationship between speakers and sessions.

This collection allows:

- One speaker to present multiple sessions
- One session to have multiple speakers
- Different speaking roles within the same session

The collection also stores event-specific information about the speaker that should not be stored in the speaker profile.

---

# Firestore Collection

speakerAssignments

---

# Purpose

The Speaker Assignments collection manages all speaker participation for event sessions.

It stores:

- Session assignment
- Speaker role
- Speaking order
- Confirmation status
- Check-in status
- Organizer notes

---

# Document ID Strategy

Firestore Auto ID

Example

speakerAssignment_01

---

# Speaker Roles

Supported values

- Keynote Speaker
- Speaker
- Co-Speaker
- Panelist
- Moderator
- Host
- Facilitator
- MC

---

# Assignment Status

Supported values

- Pending
- Invited
- Confirmed
- Declined
- Cancelled

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |

---

## Relationships

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| sessionRef | Document Reference | Yes | Assigned session |
| speakerRef | Document Reference | Yes | Assigned speaker |

---

## Assignment Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| speakerRole | String | Yes | Speaking role |
| speakingOrder | Number | No | Display order |
| status | String | Yes | Assignment status |
| confirmedAt | Timestamp | No | Confirmation date |
| checkedIn | Boolean | Yes | Checked in |
| checkedInAt | Timestamp | No | Check-in time |
| notes | String | No | Organizer notes |

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Created date |
| updatedBy | Document Reference | No | Last updated by |
| updatedAt | Timestamp | Yes | Last updated |

---

# Dependencies

## Parent Collections

- Organizations
- Events
- Sessions
- Speakers

---

## Child Collections

None

---

# Relationships

Organization

↓

Events

↓

Sessions

↓

SpeakerAssignments

↓

Speakers

---

# Business Rules

- Every assignment belongs to one organization.
- Every assignment belongs to one event.
- Every assignment references one session.
- Every assignment references one speaker.
- A speaker may appear in multiple assignments.
- A session may have multiple speaker assignments.
- A speaker cannot be assigned to the same session more than once.

---

# Validation Rules

Required

- organizationRef
- eventRef
- sessionRef
- speakerRef
- speakerRole

Validation

- Speaker must exist.
- Session must exist.
- Event must exist.
- Duplicate speaker assignments are not allowed.

---

# Security Rules

## Read

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

Super Admin

---

## Delete

Super Admin

Recommendation

Archive assignments instead of deleting them.

---

# Firestore Queries

## Speakers for Session

sessionRef == selectedSession

---

## Sessions for Speaker

speakerRef == selectedSpeaker

---

## Confirmed Speakers

status == "Confirmed"

---

## Checked-In Speakers

checkedIn == true

---

# Composite Indexes

organizationRef ASC

eventRef ASC

sessionRef ASC

speakerRef ASC

status ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| Read | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Update | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| Delete | ❌ | ❌ | ❌ | ❌ | Archive | ✅ |

---

# Used By

- Home
- Schedule
- Session Details
- Speaker Directory
- Speaker Profile
- Admin Dashboard
- Reports

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "sessionRef": "/sessions/session_01",
  "speakerRef": "/speakers/speaker_01",
  "speakerRole": "Keynote Speaker",
  "speakingOrder": 1,
  "status": "Confirmed",
  "confirmedAt": "2027-03-01T12:00:00Z",
  "checkedIn": false,
  "checkedInAt": null,
  "notes": "",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Speaker contracts
- Honorarium tracking
- Travel information
- Hotel accommodations
- Presentation submission status
- Biography approval
- Speaker onboarding checklist
- Session rehearsal scheduling
