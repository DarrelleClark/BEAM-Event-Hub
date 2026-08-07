# Tickets Collection

## Overview

The `tickets` collection stores the digital ticket issued to an attendee after a successful registration.

Each ticket belongs to one registration and serves as the attendee's credential for event check-in.

Tickets contain QR codes, ticket numbers, validity status, and lifecycle information.

---

# Firestore Collection

tickets

---

# Purpose

The Tickets collection powers:

- QR Pass
- Digital Ticket
- Event Check-In
- Badge Printing
- Ticket Validation
- Attendance Verification

---

# Document ID Strategy

Firestore Auto ID

Example

ticket_01

---

# Ticket Status

Supported values

- Active
- Checked In
- Cancelled
- Expired
- Revoked

---

# Ticket Types

Supported values

- General Admission
- VIP
- Student
- Volunteer
- Speaker
- Staff
- Sponsor
- Vendor
- Media
- Guest

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |
| registrationRef | Document Reference | Yes | Related registration |
| userRef | Document Reference | Yes | Ticket owner |

---

## Ticket Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| ticketNumber | String | Yes | Human-readable ticket number |
| ticketType | String | Yes | Ticket category |
| status | String | Yes | Ticket status |
| qrCode | String | Yes | QR code value |
| barcode | String | No | Barcode value |
| issueDate | Timestamp | Yes | Issue date |
| expirationDate | Timestamp | No | Expiration date |

---

## Validation

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| isValid | Boolean | Yes | Ticket validity |
| checkedIn | Boolean | Yes | Check-in completed |
| checkedInAt | Timestamp | No | Check-in timestamp |
| revokedAt | Timestamp | No | Revocation timestamp |

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
- Events
- Users
- Registrations

## Child Collections

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

- Every ticket belongs to one registration.
- Every ticket belongs to one event.
- Every ticket belongs to one user.
- Ticket numbers must be unique.
- QR codes must be unique.
- Revoked tickets cannot be checked in.
- Expired tickets cannot be used.
- A checked-in ticket cannot be checked in again unless manually reset.

---

# Validation Rules

Required

- organizationRef
- eventRef
- registrationRef
- userRef
- ticketNumber
- qrCode
- ticketType

Validation

- Ticket number must be unique.
- QR code must be unique.
- Registration must exist.
- User must match the registration owner.

---

# Security Rules

## Read

Users may view their own ticket.

Organization staff may view tickets for their events.

Super Admin has full access.

---

## Create

System Automation

Organization Admin

Event Manager

Super Admin

---

## Update

Organization Admin

Event Manager

Volunteer (Check-in only)

Super Admin

---

## Delete

Super Admin

Recommendation

Revoke tickets instead of deleting them.

---

# Firestore Queries

## My Ticket

userRef == currentUser

eventRef == selectedEvent

---

## Ticket by QR Code

qrCode == scannedValue

---

## Ticket by Number

ticketNumber == enteredValue

---

## Active Tickets

status == "Active"

---

## Checked-In Tickets

checkedIn == true

---

# Composite Indexes

organizationRef ASC

eventRef ASC

status ASC

---

userRef ASC

eventRef ASC

---

ticketNumber ASC

---

qrCode ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | ❌ | ❌ | ❌ | ✅ (System) | ✅ | ✅ |
| Read | Own | Own | Assigned Events | Yes | Yes | Yes |
| Update | ❌ | ❌ | Check-In Only | Yes | Yes | Yes |
| Delete | ❌ | ❌ | ❌ | ❌ | Archive | ✅ |

---

# Used By

- QR Pass
- My Tickets
- Check-In
- Home
- Profile
- Volunteer Dashboard
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "registrationRef": "/registrations/registration_01",
  "userRef": "/users/uid123",
  "ticketNumber": "BSSS-TKT-2027-000145",
  "ticketType": "General Admission",
  "status": "Active",
  "qrCode": "BSSS2027000145",
  "barcode": "",
  "issueDate": "2026-12-10T15:02:00Z",
  "expirationDate": "2027-03-22T18:00:00Z",
  "isValid": true,
  "checkedIn": false,
  "checkedInAt": null,
  "revokedAt": null,
  "notes": "",
  "createdBy": "/users/system",
  "createdAt": "2026-12-10T15:02:00Z",
  "updatedBy": "/users/system",
  "updatedAt": "2026-12-10T15:02:00Z"
}
```

---

# Future Enhancements

- Apple Wallet support
- Google Wallet support
- NFC tickets
- Badge printing
- Companion tickets
- Ticket transfers
- Offline validation
- Dynamic QR codes
- Secure encrypted QR payloads
- Multi-day ticket support
