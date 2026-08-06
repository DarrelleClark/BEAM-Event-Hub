# Tracks Collection

## Overview

The `tracks` collection organizes sessions into thematic categories within an event.

Tracks help attendees browse related sessions, filter the schedule, and understand the structure of an event.

Examples include Leadership, STEM, Career Development, College Readiness, and Wellness.

Each track belongs to a single event.

---

# Firestore Collection

tracks

---

# Purpose

The Tracks collection categorizes sessions for an event.

It provides:

- Session organization
- Schedule filtering
- Event agenda structure
- Reporting by topic
- Attendee browsing

---

# Document ID Strategy

Firestore Auto ID

Example

track_01

---

# Fields

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Organization owner |
| eventRef | Document Reference | Yes | Parent event |
| trackName | String | Yes | Track title |
| shortName | String | No | Short display name |
| description | String | No | Track description |
| icon | String | No | Material icon name or asset |
| color | String | No | Brand color (Hex) |
| sortOrder | Number | Yes | Display order |
| status | String | Yes | Track status |
| createdBy | Document Reference | Yes | Created by |
| createdAt | Timestamp | Yes | Creation timestamp |
| updatedBy | Document Reference | No | Updated by |
| updatedAt | Timestamp | Yes | Last update |

---

# Status

Allowed values

- Active
- Inactive
- Archived

---

# Relationships

Organization

↓

Events

↓

Tracks

↓

Sessions

---

# Business Rules

- Every track belongs to one organization.
- Every track belongs to one event.
- A track may contain many sessions.
- Sessions may reference only one track.
- Archived tracks cannot be assigned to new sessions.

---

# Validation Rules

- Track name is required.
- Event reference is required.
- Organization reference is required.
- Sort order must be zero or greater.

---

# Security Rules

## Read

Authenticated users

Organization staff

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

Archive tracks instead of deleting.

---

# Firestore Queries

## Tracks by Event

eventRef == selectedEvent

---

## Active Tracks

status == "Active"

---

## Tracks by Organization

organizationRef == currentOrganization

---

## Search Tracks

trackName

---

# Composite Indexes

organizationRef ASC

eventRef ASC

sortOrder ASC

status ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | No | No | No | Yes | Yes | Yes |
| Read | Yes | Yes | Yes | Yes | Yes | Yes |
| Update | No | No | No | Yes | Yes | Yes |
| Delete | No | No | No | No | Archive | Yes |

---

# Used By

- Schedule
- Session Details
- Home
- Event Management
- Session Management
- Reports

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "trackName": "Leadership",
  "shortName": "Leadership",
  "description": "Sessions focused on leadership development and community impact.",
  "icon": "groups",
  "color": "#4B2E83",
  "sortOrder": 1,
  "status": "Active",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Track icons
- Track images
- Featured tracks
- Track analytics
- Session recommendations by track
- AI-powered personalized tracks
