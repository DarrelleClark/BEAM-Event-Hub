# Vendors Collection

## Overview

The `vendors` collection stores businesses, exhibitors, recruiters, and organizations participating in an event as vendors.

Vendors typically operate booths, provide products or services, recruit attendees, or exhibit during the event.

Each vendor belongs to one organization and one event.

---

# Firestore Collection

vendors

---

# Purpose

The Vendors collection manages all event exhibitors and vendors.

It powers:

- Vendor Directory
- Vendor Details
- Expo Hall
- Booth Map
- Vendor Search
- Event Management

---

# Document ID Strategy

Firestore Auto ID

Example

vendor_01

---

# Vendor Status

Supported values

- Pending
- Approved
- Active
- Rejected
- Cancelled
- Archived

---

# Vendor Types

Supported values

- Exhibitor
- Recruiter
- College
- Nonprofit
- Government Agency
- Small Business
- Corporate
- Food Vendor
- Merchandise
- Service Provider

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |

---

## Vendor Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| vendorName | String | Yes | Vendor name |
| vendorType | String | Yes | Vendor category |
| description | String | No | Vendor description |
| logoUrl | String | No | Vendor logo |
| bannerImage | String | No | Banner image |
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
| boothNumber | String | Yes | Booth number |
| boothLocation | String | No | Booth location |
| boothSize | String | No | Booth size |
| electricityRequired | Boolean | Yes | Electrical service required |
| internetRequired | Boolean | Yes | Internet service required |

---

## Display Settings

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| featured | Boolean | Yes | Featured vendor |
| displayOrder | Number | Yes | Display order |
| status | String | Yes | Vendor status |

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
Vendors
```

---

# Business Rules

- Every vendor belongs to one organization.
- Every vendor belongs to one event.
- Booth numbers must be unique within an event.
- Archived vendors remain available for historical reporting.
- Featured vendors appear before standard vendors.

---

# Validation Rules

Required

- organizationRef
- eventRef
- vendorName
- vendorType
- boothNumber
- status

Validation

- Booth number must be unique within the event.
- Vendor name cannot be empty.

---

# Security Rules

## Read

Published vendors are visible to all attendees.

Organization staff may manage vendors for their organization.

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

Archive vendors instead of deleting them.

---

# Firestore Queries

## Vendors by Event

eventRef == selectedEvent

---

## Featured Vendors

featured == true

---

## Vendors by Type

vendorType == selectedType

---

## Active Vendors

status == "Active"

---

## Search Vendors

Search

- vendorName
- vendorType
- boothNumber

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

vendorType ASC

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

- Vendor Directory
- Vendor Details
- Expo Hall
- Home
- Event Details
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "vendorName": "Portland State University",
  "vendorType": "College",
  "description": "University admissions and student success resources.",
  "logoUrl": "",
  "bannerImage": "",
  "website": "https://www.pdx.edu",
  "contactName": "Admissions Office",
  "contactEmail": "admissions@pdx.edu",
  "contactPhone": "+1-503-725-3000",
  "boothNumber": "B-15",
  "boothLocation": "Exhibit Hall B",
  "boothSize": "10x10",
  "electricityRequired": true,
  "internetRequired": true,
  "featured": false,
  "displayOrder": 8,
  "status": "Active",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Vendor portal
- Product catalog
- Job postings
- Lead retrieval
- Appointment scheduling
- Booth analytics
- QR booth check-ins
- Vendor messaging
- Promotional offers
- Digital brochures
