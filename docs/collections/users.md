# Users Collection

## Overview

The `users` collection stores profile information for every authenticated user in BEAM Event Hub.

Authentication is managed by Firebase Authentication. This collection stores application-specific user information, organization membership, roles, permissions, preferences, and profile settings.

Each Firebase Authentication user has exactly one corresponding Firestore document.

---

# Firestore Collection

users

---

# Purpose

The Users collection serves as the central identity store for the application.

It is responsible for:

- User profiles
- Organization membership
- Authentication mapping
- Authorization
- Role management
- Permissions
- Notification preferences
- Profile settings

---

# Document ID Strategy

Document ID = Firebase Authentication UID

Example

uid_xxxxxxxxxxxxxxxxx

Using the Firebase UID as the Firestore document ID eliminates duplicate identifiers and simplifies lookups.

---

# Authentication

Provider

Firebase Authentication

Supported Providers

- Email & Password
- Google Sign-In
- Apple Sign-In (Future)
- Microsoft (Future)

---

# Primary Roles

Each user has one primary role used for routing and dashboard selection.

Available values:

- Super Admin
- Organization Admin
- Event Manager
- Volunteer
- Speaker
- Attendee

---

# Multiple Roles

A user may have multiple assigned roles.

Examples

Organization Admin + Speaker

Volunteer + Attendee

Event Manager + Speaker

Super Admin + Organization Admin

---

# Fields

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| firstName | String | Yes | User first name |
| lastName | String | Yes | User last name |
| displayName | String | Yes | Public display name |
| email | String | Yes | User email |
| phone | String | No | Contact phone |
| photoUrl | String | No | Profile photo |
| bio | String | No | Biography |
| company | String | No | Company or organization |
| jobTitle | String | No | Job title |
| website | String | No | Website |
| linkedin | String | No | LinkedIn profile |
| primaryRole | String | Yes | Default role used after login |
| roles | List<String> | Yes | All assigned roles |
| primaryOrganization | Document Reference | Yes | Default organization |
| organizations | List<Document Reference> | Yes | Organizations the user belongs to |
| permissions | List<String> | No | Additional permissions |
| status | String | Yes | Account status |
| profileComplete | Boolean | Yes | Has completed onboarding |
| timezone | String | Yes | User timezone |
| language | String | Yes | Preferred language |
| pushNotifications | Boolean | Yes | Push notifications enabled |
| emailNotifications | Boolean | Yes | Email notifications enabled |
| smsNotifications | Boolean | No | SMS notifications enabled |
| lastLogin | Timestamp | No | Last login |
| createdAt | Timestamp | Yes | Creation timestamp |
| updatedAt | Timestamp | Yes | Last update timestamp |
| createdBy | Document Reference | No | User who created this account |
| updatedBy | Document Reference | No | Last user to update |

---

# Account Status

Allowed values

- Active
- Pending
- Invited
- Suspended
- Archived

---

# Relationships

Users

├── Organizations

├── Registrations

├── Tickets

├── CheckIns

├── SpeakerAssignments

├── VolunteerAssignments

├── Favorite Sessions (Future)

└── Notifications (Future)

---

# Business Rules

- Every authenticated user must have one Firestore user document.
- Every user must belong to at least one organization.
- Every user must have one primary role.
- A user may have multiple roles.
- A user may belong to multiple organizations.
- Email addresses must be unique.
- Deleted users should be archived rather than permanently removed.

---

# Validation Rules

- Email must be unique.
- Display name cannot be empty.
- First name is required.
- Last name is required.
- Primary role is required.
- Primary organization is required.
- Status must match an allowed value.

---

# Security Rules

## Read

Users can read their own profile.

Organization Admins can read users in their organization.

Super Admins can read every user.

---

## Create

Registration Flow

Organization Admin

Super Admin

---

## Update

User (Own Profile)

Organization Admin

Super Admin

---

## Delete

Super Admin only.

Recommendation:

Archive users instead of deleting them.

---

# Firestore Queries

## Current User

Document ID == auth.uid

---

## Users by Organization

primaryOrganization == organizationRef

---

## Users by Role

roles array contains selectedRole

---

## Active Users

status == "Active"

---

## Search Users

displayName

email

company

---

# Composite Indexes

primaryOrganization ASC

status ASC

primaryRole ASC

displayName ASC

createdAt DESC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Org Admin | Super Admin |
|------------|----------|----------|------------|---------------|------------|--------------|
| Create | Registration | Registration | Registration | Registration | Yes | Yes |
| Read Own | Yes | Yes | Yes | Yes | Yes | Yes |
| Read Others | No | No | No | Organization | Organization | All |
| Update Own | Yes | Yes | Yes | Yes | Yes | Yes |
| Update Others | No | No | No | Limited | Organization | All |
| Delete | No | No | No | No | No | Yes |

---

# Used By

Authentication

Login

Register

Forgot Password

Profile

Home

Schedule

QR Pass

Speaker Dashboard

Volunteer Dashboard

Organization Dashboard

Admin Dashboard

Reports

---

# Example Document

```json
{
  "firstName": "Darrelle",
  "lastName": "Clark",
  "displayName": "Darrelle Clark",
  "email": "darrelle@example.com",
  "phone": "+1 555-555-5555",
  "photoUrl": "",
  "primaryRole": "Organization Admin",
  "roles": [
    "Organization Admin",
    "Speaker"
  ],
  "primaryOrganization": "/organizations/beam",
  "organizations": [
    "/organizations/beam"
  ],
  "permissions": [
    "manage_events",
    "manage_sessions",
    "view_reports"
  ],
  "status": "Active",
  "profileComplete": true,
  "timezone": "America/Los_Angeles",
  "language": "en",
  "pushNotifications": true,
  "emailNotifications": true,
  "smsNotifications": false,
  "lastLogin": "2026-08-06T20:00:00Z",
  "createdAt": "2026-04-01T00:00:00Z",
  "updatedAt": "2026-08-06T20:00:00Z"
}
```

---

# Future Enhancements

- Multi-factor authentication status
- User badges
- Accessibility preferences
- Theme preferences
- Social accounts
- Digital business cards
- Emergency contact
- Calendar integrations
- Activity log
- Device management
