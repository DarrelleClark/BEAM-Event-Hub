# Rooms Collection

## Overview

The `rooms` collection stores individual rooms within a venue where sessions, workshops, meetings, and other event activities take place.

Each room belongs to a single venue but may be used across multiple events.

Rooms provide scheduling, capacity management, accessibility information, and equipment details.

---

# Firestore Collection

rooms

---

# Purpose

The Rooms collection manages physical event spaces.

It provides:

- Room assignments
- Session locations
- Capacity management
- Accessibility
- Equipment inventory
- Floor information

---

# Document ID Strategy

Firestore Auto ID

Example

room_01

---

# Room Types

Supported values

- Auditorium
- Ballroom
- Classroom
- Breakout Room
- Workshop Room
- Meeting Room
- Exhibit Hall
- Outdoor Space
- Virtual Room

---

# Fields

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Organization owner |
| venueRef | Document Reference | Yes | Parent venue |
| roomName | String | Yes | Room name |
| roomCode | String | No | Internal room code |
| roomType | String | Yes | Type of room |
| floor | String | No | Floor level |
| capacity | Number | Yes | Maximum occupancy |
| description | String | No | Room description |
| imageUrl | String | No | Room image |
| hasProjector | Boolean | Yes | Projector available |
| hasMicrophones | Boolean | Yes | Microphones available |
| hasStage | Boolean | Yes | Stage available |
| hasRecording | Boolean | Yes | Recording equipment |
| hasLivestream | Boolean | Yes | Livestream capable |
| wheelchairAccessible | Boolean | Yes | ADA accessibility |
| mapReference | String | No | Indoor map reference |
| status | String | Yes | Room availability |
| createdBy | Document Reference | Yes | Created by |
| createdAt | Timestamp | Yes | Creation timestamp |
| updatedBy | Document Reference | No | Updated by |
| updatedAt | Timestamp | Yes | Last update |

---

# Status

Allowed values

- Available
- Reserved
- Closed
- Maintenance
- Archived

---

# Relationships

Organization

↓

Venue

↓

Rooms

↓

Sessions

---

# Business Rules

- Every room belongs to one venue.
- Every room belongs to one organization.
- Capacity must be greater than zero.
- Archived rooms cannot be assigned to sessions.
- Multiple sessions cannot occupy the same room at the same time.

---

# Validation Rules

- Room name is required.
- Venue reference is required.
- Organization reference is required.
- Capacity must be greater than zero.

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

Archive rooms instead of deleting.

---

# Firestore Queries

## Rooms by Venue

venueRef == selectedVenue

---

## Available Rooms

status == "Available"

---

## Rooms by Organization

organizationRef == currentOrganization

---

## Search Rooms

roomName

roomCode

---

# Composite Indexes

organizationRef ASC

venueRef ASC

status ASC

roomName ASC

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
- Venue Page
- Event Management
- Session Management
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "venueRef": "/venues/venue_01",
  "roomName": "Ballroom A",
  "roomCode": "A101",
  "roomType": "Ballroom",
  "floor": "1",
  "capacity": 500,
  "description": "Main keynote ballroom.",
  "imageUrl": "",
  "hasProjector": true,
  "hasMicrophones": true,
  "hasStage": true,
  "hasRecording": true,
  "hasLivestream": true,
  "wheelchairAccessible": true,
  "mapReference": "Floor1-A101",
  "status": "Available",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Indoor navigation
- Seat maps
- Smart room occupancy
- Digital signage integration
- QR room check-in
- Live room status
- Environmental sensors
- Equipment inventory tracking
