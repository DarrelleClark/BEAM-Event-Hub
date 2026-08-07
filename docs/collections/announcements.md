# Announcements Collection

## Overview

The `announcements` collection stores communications sent to users before, during, and after an event.

Announcements may be displayed within the application, delivered as push notifications, or both.

Announcements can target specific audiences and be scheduled for future publication.

---

# Firestore Collection

announcements

---

# Purpose

The Announcements collection powers:

- Home Dashboard
- Announcement Center
- Push Notifications
- Emergency Alerts
- Event Updates
- Schedule Changes
- Volunteer Communications
- Speaker Communications

---

# Document ID Strategy

Firestore Auto ID

Example

announcement_01

---

# Announcement Status

Supported values

- Draft
- Scheduled
- Published
- Expired
- Archived

---

# Announcement Priority

Supported values

- Low
- Normal
- High
- Critical

---

# Audience Types

Supported values

- Everyone
- Attendees
- Speakers
- Volunteers
- Vendors
- Sponsors
- Event Managers
- Organization Admins

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |

---

## Announcement

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| title | String | Yes | Announcement title |
| message | String | Yes | Announcement body |
| imageUrl | String | No | Optional image |
| priority | String | Yes | Announcement priority |
| status | String | Yes | Announcement status |

---

## Audience

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| audience | List<String> | Yes | Target audiences |
| sendPushNotification | Boolean | Yes | Send push notification |
| sendInAppNotification | Boolean | Yes | Display in app |
| pinned | Boolean | Yes | Pin to top |

---

## Schedule

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| publishAt | Timestamp | Yes | Publish date/time |
| expireAt | Timestamp | No | Expiration date/time |

---

## Analytics

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| totalViews | Number | Yes | Number of views |
| totalClicks | Number | Yes | Number of clicks |

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Creation date |
| updatedBy | Document Reference | No | Last editor |
| updatedAt | Timestamp | Yes | Last update |

---

# Dependencies

## Parent Collections

- Organizations
- Events

## Child Collections

None

---

# Relationships

```
Organization
      │
      ▼
Events
      │
      ▼
Announcements
```

---

# Business Rules

- Every announcement belongs to one organization.
- Every announcement belongs to one event.
- An announcement may target multiple audiences.
- Scheduled announcements are automatically published.
- Expired announcements are hidden from users.
- Critical announcements always appear at the top.

---

# Validation Rules

Required

- organizationRef
- eventRef
- title
- message
- priority
- audience
- publishAt

Validation

- Title cannot be empty.
- Publish date cannot be in the past when creating scheduled announcements.
- Expiration date must be after publish date.

---

# Security Rules

## Read

Published announcements are visible to users included in the target audience.

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

Archive announcements instead of deleting them.

---

# Firestore Queries

## Current Announcements

status == "Published"

---

## Pinned Announcements

pinned == true

---

## Announcements by Event

eventRef == selectedEvent

---

## Scheduled Announcements

status == "Scheduled"

---

## Critical Announcements

priority == "Critical"

---

# Composite Indexes

organizationRef ASC

eventRef ASC

publishAt DESC

---

status ASC

publishAt DESC

---

priority ASC

publishAt DESC

---

pinned ASC

publishAt DESC

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
- Announcement Center
- Notifications
- Volunteer Dashboard
- Speaker Dashboard
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "title": "Welcome to the Black Student Success Summit!",
  "message": "Registration opens at 8:00 AM. Please have your QR Pass ready before arriving at the entrance.",
  "imageUrl": "",
  "priority": "High",
  "status": "Published",
  "audience": [
    "Everyone"
  ],
  "sendPushNotification": true,
  "sendInAppNotification": true,
  "pinned": true,
  "publishAt": "2027-03-20T07:00:00Z",
  "expireAt": "2027-03-22T18:00:00Z",
  "totalViews": 0,
  "totalClicks": 0,
  "createdBy": "/users/uid123",
  "createdAt": "2027-03-19T20:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2027-03-19T20:00:00Z"
}
```

---

# Future Enhancements

- Rich text editor
- Images and videos
- Deep links
- Read receipts
- Emoji reactions
- Scheduled recurring announcements
- Multi-language support
- AI-generated announcements
- Audience segmentation
- Delivery analytics
