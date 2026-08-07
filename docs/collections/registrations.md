# Registrations Collection

## Overview

The `registrations` collection stores attendee registrations for events.

A registration represents a user's intent to attend an event and tracks their registration status throughout the event lifecycle.

Each registration belongs to one user and one event.

A registration may later generate one ticket and one or more check-in records.

---

# Firestore Collection

registrations

---

# Purpose

The Registrations collection manages the attendee registration process.

It powers:

- Event Registration
- My Events
- My Tickets
- QR Pass
- Check-In
- Attendance Reports

---

# Document ID Strategy

Firestore Auto ID

Example

registration_01

---

# Registration Status

Supported values

- Pending
- Confirmed
- Waitlisted
- Cancelled
- Checked In
- No Show

---

# Registration Source

Supported values

- Mobile App
- Website
- Admin
- Volunteer
- Import
- API

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |
| userRef | Document Reference | Yes | Registered attendee |

---

## Registration Details

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| registrationNumber | String | Yes | Human-readable registration ID |
| status | String | Yes | Registration status |
| source | String | Yes | Registration source |
| ticketType | String | Yes | Ticket category |
| registrationDate | Timestamp | Yes | Registration date |
| confirmedAt | Timestamp | No | Confirmation timestamp |
| cancelledAt | Timestamp | No | Cancellation timestamp |

---

## Payment

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| paymentRequired | Boolean | Yes | Payment required |
| paymentStatus | String | Yes | Payment status |
| paymentAmount | Number | No | Amount paid |
| currency | String | No | Currency code |

---

# Payment Status

Supported values

- Not Required
- Pending
- Paid
- Refunded
- Failed

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| notes | String | No | Internal notes |
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Created date |
| updatedBy | Document Reference | No | Last updated by |
| updatedAt | Timestamp | Yes | Last update |

---

# Dependencies

## Parent Collections

- Organizations
- Users
- Events

## Child Collections

- Tickets
- CheckIns

---

# Relationships

Organization

↓

Events

↓

Registrations

↓

Tickets

↓

CheckIns

---

# Business Rules

- A user may only have one active registration per event.
- Every registration belongs to one event.
- Every registration belongs to one user.
- Registration numbers must be unique.
- Cancelled registrations cannot generate tickets.
- Waitlisted registrations do not receive tickets until confirmed.

---

# Validation Rules

Required

- organizationRef
- eventRef
- userRef
- registrationNumber
- ticketType
- registrationDate

Validation

- Duplicate registrations for the same user and event are not allowed.
- Registration status must match an allowed value.

---

# Security Rules

## Read

Users may view their own registrations.

Organization staff may view registrations for their events.

Super Admin has full access.

---

## Create

User (Self Registration)

Volunteer

Event Manager

Organization Admin

Super Admin

---

## Update

Organization Admin

Event Manager

Volunteer (Limited)

Super Admin

---

## Delete

Super Admin

Recommendation

Cancel registrations instead of deleting them.

---

# Firestore Queries

## My Registrations

userRef == currentUser

---

## Event Registrations

eventRef == selectedEvent

---

## Confirmed Registrations

status == "Confirmed"

---

## Waitlisted Registrations

status == "Waitlisted"

---

## Checked-In Attendees

status == "Checked In"

---

# Composite Indexes

organizationRef ASC

eventRef ASC

status ASC

---

userRef ASC

registrationDate DESC

---

eventRef ASC

registrationDate DESC

---

eventRef ASC

ticketType ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | ✅ Self | ✅ Self | ✅ | ✅ | ✅ | ✅ |
| Read | Own | Own | Assigned Events | Yes | Yes | Yes |
| Update | Cancel Own* | Own* | Limited | Yes | Yes | Yes |
| Delete | ❌ | ❌ | ❌ | ❌ | Archive | ✅ |

*Subject to event registration policies.

---

# Used By

- Event Details
- Registration
- Home
- Profile
- QR Pass
- My Tickets
- Admin Dashboard
- Reports

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "userRef": "/users/uid123",
  "registrationNumber": "BSSS-2027-000145",
  "status": "Confirmed",
  "source": "Mobile App",
  "ticketType": "General Admission",
  "registrationDate": "2026-12-10T15:00:00Z",
  "confirmedAt": "2026-12-10T15:01:00Z",
  "paymentRequired": false,
  "paymentStatus": "Not Required",
  "paymentAmount": 0,
  "currency": "USD",
  "notes": "",
  "createdBy": "/users/uid123",
  "createdAt": "2026-12-10T15:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-12-10T15:01:00Z"
}
```

---

# Future Enhancements

- Promotional codes
- Group registrations
- Guest registrations
- Registration questionnaires
- Digital waivers
- Emergency contacts
- Meal preferences
- Accessibility accommodations
- Waitlist automation
- Attendance certificates
