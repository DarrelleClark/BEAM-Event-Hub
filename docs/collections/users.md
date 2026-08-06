# Users Collection

## Overview

The `users` collection stores profile information for every authenticated user in BEAM Event Hub.

Authentication is handled by Firebase Authentication. This collection stores application-specific profile data, roles, permissions, and organization membership.

---

# Firestore Collection

users

---

# Purpose

Store user profiles and control access throughout the application.

Each authenticated user has exactly one document in this collection.

---

# Authentication

Provider

Firebase Authentication

Primary Identifier

Firebase Authentication UID

Document ID

Use the Firebase Authentication UID as the Firestore document ID.

Example

uid: 5YQfN4nLmP8rXz9AbC

---

# User Roles

- Super Admin
- Organization Admin
- Event Manager
- Volunteer
- Speaker
- Attendee

---

# Fields

| Field | Type | Required | Description |
|---------|------|----------|-------------|
| firstName | String | Yes | First name |
| lastName | String | Yes | Last name |
| displayName | String | Yes | Display name |
| email | String | Yes | User email |
| phone | String | No | Phone number |
| photoUrl | String | No | Profile photo |
| role | String | Yes | User role |
| organizationRef | Document Reference | Yes | Organization |
| jobTitle | String | No | Job title |
| company | String | No | Company or organization |
| bio | String | No | Biography |
| website | String | No | Website |
| linkedin | String | No | LinkedIn profile |
| timezone | String | Yes | User timezone |
| language | String | Yes | Preferred language |
| notificationsEnabled | Boolean | Yes | Push notifications |
| emailNotifications | Boolean | Yes | Email notifications |
| isActive | Boolean | Yes | Active account |
| lastLogin | Timestamp | No | Last login |
| createdAt | Timestamp | Yes | Created date |
| updatedAt | Timestamp | Yes | Updated date |
| createdBy | Document Reference | No | Created by admin |
| updatedBy | Document Reference | No | Last updated by |

---

# Relationships

User

├── Registrations

├── Tickets

├── CheckIns

├── SpeakerAssignments

├── VolunteerAssignments

└── Organization

---

# Used By

- Login
- Register
- Forgot Password
- Home
- Profile
- Schedule
- QR Pass
- Admin Dashboard
- Volunteer Dashboard
- Speaker Dashboard

---

# Firestore Queries

## Current User

Filter

Document ID == auth.uid

---

## Users by Organization

Filter

organizationRef == currentOrganization

---

## Users by Role

Filter

role == selectedRole

---

## Active Users

Filter

isActive == true

---

## Search Users

Search

displayName

email

---

# CRUD Operations

Create

✔ Firebase Authentication

✔ Registration Flow

Read

✔ Authenticated User (own profile)

✔ Organization Admin

✔ Super Admin

Update

✔ User (own profile)

✔ Organization Admin

✔ Super Admin

Delete

✔ Super Admin

---

# Security Rules

Read

Authenticated user can read their own document.

Organization Admin can read users in their organization.

Super Admin has full access.

---

Write

User may update their own profile.

Organization Admin may update users within their organization.

Super Admin may update all users.

---

Delete

Super Admin only.

---

# Composite Indexes

organizationRef ASC

role ASC

isActive ASC

displayName ASC

createdAt DESC

---

# Validation Rules

Email must be unique.

Display name cannot be empty.

Role must be one of:

- Super Admin
- Organization Admin
- Event Manager
- Volunteer
- Speaker
- Attendee

organizationRef is required.

---

# Future Expansion

- MFA status
- Last device
- User preferences
- Accessibility settings
- Social accounts
- Badge printing preferences
- Digital business cards
