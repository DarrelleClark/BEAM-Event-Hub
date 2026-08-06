# Speakers Collection

## Overview

The `speakers` collection stores information about individuals presenting or participating in event sessions.

A speaker may present multiple sessions across multiple events and organizations.

Speaker participation in sessions is managed through the `speakerAssignments` collection.

---

# Firestore Collection

speakers

---

# Purpose

The Speakers collection stores public-facing speaker profiles and professional information.

It powers:

- Speaker Directory
- Speaker Profile
- Session Details
- Home Page
- Featured Speakers

---

# Document ID Strategy

Firestore Auto ID

Example

speaker_01

---

# Speaker Status

Supported values

- Invited
- Confirmed
- Declined
- Cancelled
- Archived

---

# Fields

## Ownership

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Parent organization |

---

## Profile

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| firstName | String | Yes | First name |
| lastName | String | Yes | Last name |
| displayName | String | Yes | Public display name |
| title | String | No | Professional title |
| organization | String | No | Company or organization |
| biography | String | Yes | Biography |
| profilePhoto | String | No | Photo URL |
| email | String | No | Contact email |
| phone | String | No | Contact phone |
| website | String | No | Website |
| linkedin | String | No | LinkedIn profile |
| twitter | String | No | X/Twitter profile |

---

## Presentation

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| expertise | List<String> | No | Areas of expertise |
| featured | Boolean | Yes | Featured speaker |
| status | String | Yes | Current status |

---

## Metadata

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Creation timestamp |
| updatedBy | Document Reference | No | Last updated by |
| updatedAt | Timestamp | Yes | Last update |

---

# Relationships

Organization

↓

Speakers

↓

SpeakerAssignments

↓

Sessions

---

# Dependencies

## Parent Collections

- Organizations

## Child Collections

- SpeakerAssignments

---

# Business Rules

- A speaker belongs to one organization.
- A speaker may present multiple sessions.
- Multiple speakers may present one session.
- Speakers remain in the database after an event concludes.
- Archived speakers cannot be assigned to new sessions.

---

# Validation Rules

Required

- firstName
- lastName
- displayName
- biography

---

# Security Rules

## Read

Published speaker profiles

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

Speaker (Own Profile)

Super Admin

---

## Delete

Super Admin

Recommendation

Archive speakers instead of deleting.

---

# Firestore Queries

## Featured Speakers

featured == true

---

## Speakers by Organization

organizationRef == currentOrganization

---

## Search Speakers

Search

- displayName
- organization
- expertise

---

# Composite Indexes

organizationRef ASC

featured ASC

displayName ASC

status ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| Read | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Update | ❌ | Own Profile | ❌ | ✅ | ✅ | ✅ |
| Delete | ❌ | ❌ | ❌ | ❌ | Archive | ✅ |

---

# Used By

- Home
- Speaker Directory
- Speaker Profile
- Session Details
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "firstName": "Jane",
  "lastName": "Smith",
  "displayName": "Dr. Jane Smith",
  "title": "Executive Director",
  "organization": "BEAM Village",
  "biography": "National education leader focused on Black student success.",
  "profilePhoto": "",
  "email": "jane@example.org",
  "website": "",
  "linkedin": "",
  "twitter": "",
  "expertise": [
    "Leadership",
    "Education",
    "Equity"
  ],
  "featured": true,
  "status": "Confirmed",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Speaker awards
- Pronouns
- Languages spoken
- Session ratings
- Speaker availability
- Digital business cards
- AI-generated biographies
- Video introductions
- Calendar availability
