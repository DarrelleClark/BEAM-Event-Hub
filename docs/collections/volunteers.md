# Volunteers Collection

## Overview

The `volunteers` collection stores volunteer assignments for specific events.

Unlike the `users` collection, which stores permanent user accounts, the Volunteers collection represents a user's participation as a volunteer for a particular event.

A user may volunteer for multiple events.

Each volunteer record belongs to one user and one event.

---

# Firestore Collection

volunteers

---

# Purpose

The Volunteers collection manages all volunteers participating in an event.

It powers:

- Volunteer Dashboard
- Volunteer Check-In
- Shift Management
- Task Assignments
- Volunteer Reports
- Hours Tracking

---

# Document ID Strategy

Firestore Auto ID

Example

volunteer_01

---

# Volunteer Status

Supported values

- Invited
- Pending
- Confirmed
- Checked In
- Active
- Completed
- Cancelled
- Archived

---

# Volunteer Departments

Supported values

- Registration
- Check-In
- Information Desk
- Speaker Support
- Room Monitor
- Logistics
- Hospitality
- Security
- Photography
- Technical Support
- Stage Management
- Vendor Support

---

# Volunteer Roles

Supported values

- Volunteer
- Team Lead
- Coordinator
- Supervisor

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |
| eventRef | Document Reference | Yes | Parent event |
| userRef | Document Reference | Yes | Volunteer user |

---

## Volunteer Information

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| volunteerRole | String | Yes | Volunteer role |
| department | String | Yes | Assigned department |
| shiftName | String | No | Shift name |
| shiftStart | Timestamp | Yes | Shift start |
| shiftEnd | Timestamp | Yes | Shift end |
| supervisorRef | Document Reference | No | Supervisor |
| status | String | Yes | Volunteer status |

---

## Event Activity

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| checkedIn | Boolean | Yes | Volunteer checked in |
| checkedInAt | Timestamp | No | Check-in time |
| checkedOut | Boolean | Yes | Volunteer checked out |
| checkedOutAt | Timestamp | No | Check-out time |
| hoursWorked | Number | No | Total hours worked |

---

## Notes

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| emergencyContact | String | No | Emergency contact |
| emergencyPhone | String | No | Emergency phone |
| notes | String | No | Internal notes |

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Creation date |
| updatedBy | Document Reference | No | Last updated by |
| updatedAt | Timestamp | Yes | Last update |

---

# Dependencies

## Parent Collections

- Organizations
- Events
- Users

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
Volunteers
      │
      ▼
Users
```

---

# Business Rules

- Every volunteer belongs to one organization.
- Every volunteer belongs to one event.
- Every volunteer references one user.
- A user may volunteer for multiple events.
- A volunteer may have only one active assignment for an event.
- Hours worked cannot be negative.
- Shift end must occur after shift start.

---

# Validation Rules

Required

- organizationRef
- eventRef
- userRef
- volunteerRole
- department
- shiftStart
- shiftEnd
- status

Validation

- Shift end must be later than shift start.
- Volunteer role must match an approved value.

---

# Security Rules

## Read

Volunteer may view their own assignment.

Organization staff may manage volunteers.

Super Admin has full access.

---

## Create

Organization Admin

Event Manager

Volunteer Coordinator

Super Admin

---

## Update

Volunteer (limited fields)

Volunteer Coordinator

Organization Admin

Super Admin

---

## Delete

Super Admin

Recommendation

Archive volunteer records instead of deleting them.

---

# Firestore Queries

## Volunteers by Event

eventRef == selectedEvent

---

## Volunteers by Department

department == selectedDepartment

---

## Volunteers by Shift

shiftStart >= today

---

## Active Volunteers

status == "Active"

---

## My Volunteer Assignment

userRef == currentUser

---

# Composite Indexes

organizationRef ASC

eventRef ASC

department ASC

---

eventRef ASC

status ASC

---

userRef ASC

eventRef ASC

---

shiftStart ASC

status ASC

---

# CRUD Operations

| Operation | Attendee | Volunteer | Coordinator | Event Manager | Organization Admin | Super Admin |
|------------|-----------|------------|--------------|---------------|--------------------|-------------|
| Create | ❌ | ❌ | ✅ | ✅ | ✅ | ✅ |
| Read | ❌ | Own | ✅ | ✅ | ✅ | ✅ |
| Update | ❌ | Limited | ✅ | ✅ | ✅ | ✅ |
| Delete | ❌ | ❌ | ❌ | ❌ | Archive | ✅ |

---

# Used By

- Volunteer Dashboard
- Check-In
- Admin Dashboard
- Event Management
- Reports

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventRef": "/events/event_01",
  "userRef": "/users/uid456",
  "volunteerRole": "Volunteer",
  "department": "Check-In",
  "shiftName": "Morning Shift",
  "shiftStart": "2027-03-20T07:00:00Z",
  "shiftEnd": "2027-03-20T12:00:00Z",
  "supervisorRef": "/users/uid789",
  "status": "Confirmed",
  "checkedIn": false,
  "checkedOut": false,
  "hoursWorked": 0,
  "emergencyContact": "John Smith",
  "emergencyPhone": "+1-555-555-1234",
  "notes": "",
  "createdBy": "/users/uid123",
  "createdAt": "2026-12-01T15:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-12-01T15:00:00Z"
}
```

---

# Future Enhancements

- Volunteer certifications
- Shift swapping
- Task management
- QR volunteer badges
- Time tracking
- Performance reviews
- Volunteer messaging
- Push notifications
- Automatic shift reminders
- Volunteer rewards
