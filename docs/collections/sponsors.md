# Sponsors Collection

## Overview

The `sponsors` collection stores organizations and businesses that financially or strategically support an event.

Sponsors are displayed throughout the application, including the Home page, Sponsor Directory, Event Details, and Sponsor Profile.

Sponsors may be assigned sponsorship tiers such as Platinum, Gold, Silver, or Bronze.

---

# Firestore Collection

sponsors

---

# Purpose

The Sponsors collection manages sponsor information and event sponsorships.

It powers:

- Sponsor Directory
- Home Page Sponsor Carousel
- Sponsor Details
- Event Branding
- Sponsor Recognition
- Sponsor Analytics

---

# Document ID Strategy

Firestore Auto ID

Example

sponsor_01

---

# Sponsor Status

Supported values

- Active
- Pending
- Confirmed
- Inactive
- Archived

---

# Sponsorship Levels

Supported values

- Title Sponsor
- Presenting Sponsor
- Platinum
- Gold
- Silver
- Bronze
- Community Partner
- Media Partner
- Supporting Sponsor

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Sponsored event |

---

## Sponsor Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| sponsorName | String | Yes | Sponsor name |
| sponsorshipLevel | String | Yes | Sponsorship tier |
| description | String | No | Sponsor description |
| logoUrl | String | No | Sponsor logo |
| bannerImage | String | No | Sponsor banner |
| website | String | No | Website URL |

---

## Contact Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| contactName | String | No | Primary contact |
| contactEmail | String | No | Contact email |
| contactPhone | String | No | Contact phone |

---

## Booth Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| hasBooth | Boolean | Yes | Sponsor has booth |
| boothNumber | String | No | Booth identifier |
| boothLocation | String | No | Booth location |

---

## Display Settings

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| featured | Boolean | Yes | Featured sponsor |
| displayOrder | Number | Yes | Display order |
| status | String | Yes | Sponsor status |

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
Sponsors
```

---

# Business Rules

- Every sponsor belongs to one organization.
- Every sponsor belongs to one event.
- Sponsorship level must match an approved tier.
- Featured sponsors appear before standard sponsors.
- Archived sponsors remain in historical reports.

---

# Validation Rules

Required

- organizationRef
- eventRef
- sponsorName
- sponsorshipLevel
- status

Validation

- Sponsor name cannot be empty.
- Display order must be zero or greater.

---

# Security Rules

## Read

Everyone may view active sponsors for published events.

Organization staff may manage sponsors for their organization.

Super Admin has full access.

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

Archive sponsors instead of deleting them.

---

# Firestore Queries

## Sponsors by Event

eventRef == selectedEvent

---

## Featured Sponsors

featured == true

---

## Sponsors by Level

sponsorshipLevel == selectedLevel

---

## Active Sponsors

status == "Active"

---

# Composite Indexes

organizationRef ASC

eventRef ASC

displayOrder ASC

---

featured ASC

displayOrder ASC

---

status ASC

displayOrder ASC

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
- Sponsor Directory
- Sponsor Details
- Event Details
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "sponsorName": "Microsoft",
  "sponsorshipLevel": "Platinum",
  "description": "Supporting innovation and educational technology.",
  "logoUrl": "",
  "bannerImage": "",
  "website": "https://microsoft.com",
  "contactName": "Jane Doe",
  "contactEmail": "jane@microsoft.com",
  "contactPhone": "+1-555-555-5555",
  "hasBooth": true,
  "boothNumber": "P-12",
  "boothLocation": "Exhibit Hall A",
  "featured": true,
  "displayOrder": 1,
  "status": "Active",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Sponsor portal
- Sponsor advertisements
- Lead retrieval
- Sponsor analytics
- Digital coupons
- Sponsor giveaways
- Sponsored sessions
- Push notifications
- Booth traffic analytics
- Sponsor contracts
