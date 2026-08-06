# Events Collection

## Overview

The `events` collection stores all event information managed within BEAM Event Hub.

Every conference, summit, workshop, webinar, career fair, networking event, or educational program is represented by an Event document.

The Event serves as the parent record for sessions, registrations, tickets, speakers, volunteers, sponsors, vendors, announcements, and check-ins.

---

# Firestore Collection

events

---

# Purpose

The Events collection is the central hub of the application.

It defines:

- Event details
- Registration periods
- Event schedule
- Branding
- Venue
- Capacity
- Visibility
- Status

---

# Document ID Strategy

Firestore Auto ID

Example

event_01

---

# Event Types

Supported event types

- Conference
- Summit
- Workshop
- Seminar
- Networking Event
- Career Fair
- Training
- Webinar
- Community Event
- Fundraiser
- Graduation
- Competition

---

# Event Status

Allowed values

- Draft
- Published
- Registration Open
- Registration Closed
- In Progress
- Completed
- Cancelled
- Archived

---

# Visibility

Allowed values

- Public
- Private
- Invitation Only

---

# Fields

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Organization that owns the event |
| eventName | String | Yes | Event title |
| shortName | String | No | Short display name |
| description | String | Yes | Full description |
| eventType | String | Yes | Event type |
| status | String | Yes | Event status |
| visibility | String | Yes | Public or private |
| bannerImage | String | No | Banner image URL |
| logoImage | String | No | Event logo |
| venueRef | Document Reference | Yes | Event venue |
| startDate | Timestamp | Yes | Event start |
| endDate | Timestamp | Yes | Event end |
| timezone | String | Yes | Event timezone |
| registrationOpen | Timestamp | Yes | Registration opens |
| registrationClose | Timestamp | Yes | Registration closes |
| capacity | Number | No | Maximum attendees |
| waitlistEnabled | Boolean | Yes | Enable waitlist |
| allowWalkIns | Boolean | Yes | Allow walk-ins |
| featured | Boolean | Yes | Featured event |
| tags | List<String> | No | Search keywords |
| contactEmail | String | No | Event contact |
| contactPhone | String | No | Event phone |
| website | String | No | Event website |
| createdBy | Document Reference | Yes | User that created event |
| createdAt | Timestamp | Yes | Created timestamp |
| updatedBy | Document Reference | No | Last updated by |
| updatedAt | Timestamp | Yes | Updated timestamp |

---

# Relationships

Event

├── Sessions

├── Registrations

├── Tickets

├── CheckIns

├── Speakers

├── SpeakerAssignments

├── Sponsors

├── Vendors

├── Volunteers

├── Announcements

├── Rooms

└── Tracks

---

# Business Rules

- Every event belongs to one organization.
- Every session belongs to one event.
- Registration must open before the event starts.
- Registration must close before the event begins unless walk-ins are enabled.
- End date must be after the start date.
- Capacity cannot be negative.
- Archived events cannot be edited.
- Published events appear in attendee searches.

---

# Validation Rules

- Event name is required.
- Event type is required.
- Venue is required.
- Start date is required.
- End date is required.
- Registration dates must be valid.
- Organization reference is required.

---

# Security Rules

## Read

Published public events

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

Recommendation:

Archive instead of deleting.

---

# Firestore Queries

## Current Event

status == "In Progress"

---

## Upcoming Events

startDate > today

status == "Published"

---

## Published Events

status == "Published"

---

## Featured Events

featured == true

---

## Events by Organization

organizationRef == organization

---

## Public Events

visibility == "Public"

---

# Composite Indexes

organizationRef ASC

status ASC

startDate ASC

featured ASC

organizationRef ASC

startDate DESC

visibility ASC

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

Authentication

Home

Schedule

Event Details

QR Pass

Registration

Announcements

Sponsors

Venue

Volunteer Dashboard

Admin Dashboard

Reports

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "eventName": "Black Student Success Summit 2027",
  "shortName": "BSSS 2027",
  "description": "An annual summit dedicated to advancing educational success for Black students.",
  "eventType": "Summit",
  "status": "Published",
  "visibility": "Public",
  "bannerImage": "",
  "logoImage": "",
  "venueRef": "/venues/moda_center",
  "startDate": "2027-03-20T08:00:00Z",
  "endDate": "2027-03-22T17:00:00Z",
  "timezone": "America/Los_Angeles",
  "registrationOpen": "2026-12-01T00:00:00Z",
  "registrationClose": "2027-03-18T23:59:00Z",
  "capacity": 1200,
  "waitlistEnabled": true,
  "allowWalkIns": false,
  "featured": true,
  "tags": [
    "Education",
    "Leadership",
    "College",
    "STEM"
  ],
  "contactEmail": "events@beamvillage.org",
  "contactPhone": "+1-503-555-0100",
  "website": "https://beamvillage.org",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Recurring events
- Multi-language event content
- Virtual and hybrid events
- Livestream integration
- Event themes
- AI-generated agendas
- Calendar synchronization
- Digital certificates
- Event feedback and surveys
- Event analytics dashboard
