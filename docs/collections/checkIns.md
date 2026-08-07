# CheckIns Collection

## Overview

The `checkIns` collection records every attendee check-in activity throughout an event.

Unlike the `tickets` collection, which stores the current ticket status, the CheckIns collection stores the complete attendance history.

Each check-in represents a single scan or attendance event.

Multiple check-ins may exist for the same ticket.

---

# Firestore Collection

checkIns

---

# Purpose

The CheckIns collection powers:

- Event Entry
- Session Attendance
- QR Scanning
- Volunteer Check-In
- Attendance Reports
- Live Attendance Dashboard
- Event Analytics

---

# Document ID Strategy

Firestore Auto ID

Example

checkin_01

---

# Check-In Types

Supported values

- Event Entry
- Event Exit
- Session Entry
- Session Exit
- VIP Entry
- Vendor Entry
- Speaker Check-In
- Volunteer Check-In
- Staff Check-In

---

# Check-In Status

Supported values

- Successful
- Denied
- Duplicate
- Expired Ticket
- Invalid Ticket
- Cancelled Registration
- Revoked Ticket

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |

---

## References

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| registrationRef | Document Reference | Yes | Related registration |
| ticketRef | Document Reference | Yes | Related ticket |
| userRef | Document Reference | Yes | Attendee |
| sessionRef | Document Reference | No | Session attended |
| roomRef | Document Reference | No | Room where check-in occurred |
| venueRef | Document Reference | Yes | Venue |

---

## Check-In Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| checkInType | String | Yes | Type of check-in |
| status | String | Yes | Check-in result |
| checkInTime | Timestamp | Yes | Scan timestamp |
| scannedBy | Document Reference | Yes | Volunteer or staff member |
| scannerDevice | String | No | Device identifier |
| scannerLocation | String | No | Scan location |
| notes | String | No | Internal notes |

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| createdAt | Timestamp | Yes | Creation timestamp |
| updatedAt | Timestamp | Yes | Last update |

---

# Dependencies

## Parent Collections

- Organizations
- Events
- Users
- Registrations
- Tickets
- Sessions (Optional)

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
Registrations
      │
      ▼
Tickets
      │
      ▼
CheckIns
```

---

# Business Rules

- Every check-in belongs to one organization.
- Every check-in belongs to one event.
- Every check-in belongs to one registration.
- Every check-in belongs to one ticket.
- Every check-in belongs to one attendee.
- A ticket may have multiple check-ins.
- Check-ins are immutable and should never be edited after creation.
- Invalid tickets create a denied check-in record.

---

# Validation Rules

Required

- organizationRef
- eventRef
- registrationRef
- ticketRef
- userRef
- venueRef
- checkInType
- status
- checkInTime
- scannedBy

Validation

- Ticket must exist.
- Registration must exist.
- User must match the registration.
- Ticket must not be revoked.
- Registration must not be cancelled.

---

# Security Rules

## Read

Organization Staff

Event Managers

Organization Admins

Super Admin

Attendees may view only their own check-in history.

---

## Create

Volunteer

Event Manager

Organization Admin

Super Admin

QR Scanner Automation

---

## Update

Not permitted.

Check-ins should never be modified.

---

## Delete

Super Admin only.

Recommendation

Never delete check-ins.

Maintain them as an audit log.

---

# Firestore Queries

## Event Attendance

eventRef == selectedEvent

---

## User Check-Ins

userRef == currentUser

---

## Session Attendance

sessionRef == selectedSession

---

## Today's Check-Ins

checkInTime >= today

---

## Successful Check-Ins

status == "Successful"

---

## Failed Check-Ins

status != "Successful"

---

# Composite Indexes

organizationRef ASC

eventRef ASC

checkInTime DESC

---

ticketRef ASC

checkInTime DESC

---

userRef ASC

checkInTime DESC

---

sessionRef ASC

checkInTime DESC

---

status ASC

checkInTime DESC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | ❌ | ❌ | ✅ | ✅ | ✅ | ✅ |
| Read | Own | Own | Assigned Events | ✅ | ✅ | ✅ |
| Update | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Delete | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |

---

# Used By

- QR Pass
- Event Check-In
- Volunteer Dashboard
- Admin Dashboard
- Attendance Reports
- Analytics

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "registrationRef": "/registrations/registration_01",
  "ticketRef": "/tickets/ticket_01",
  "userRef": "/users/uid123",
  "sessionRef": null,
  "roomRef": null,
  "venueRef": "/venues/venue_01",
  "checkInType": "Event Entry",
  "status": "Successful",
  "checkInTime": "2027-03-20T08:15:32Z",
  "scannedBy": "/users/volunteer_01",
  "scannerDevice": "iPad-Entrance-01",
  "scannerLocation": "Main Entrance",
  "notes": "",
  "createdAt": "2027-03-20T08:15:32Z",
  "updatedAt": "2027-03-20T08:15:32Z"
}
```

---

# Future Enhancements

- Offline scanning
- NFC badge scanning
- Face recognition check-in
- GPS validation
- Multi-gate entry
- Live attendance dashboards
- Attendance heat maps
- Automatic session attendance
- Badge printing integration
- Fraud detection
