# Organizations Collection

## Overview

The `organizations` collection stores all organizations that use BEAM Event Hub.

An organization owns events, users, speakers, volunteers, sponsors, vendors, announcements, and reports.

---

# Firestore Collection

organizations

---

# Purpose

Provide multi-organization support.

Every record throughout the application belongs to an organization.

---

# Document ID

Firestore Auto ID

Example

organization_01

---

# Fields

| Field | Type | Required | Description |
|---------|------|----------|-------------|
| organizationName | String | Yes | Organization name |
| shortName | String | No | Short display name |
| description | String | No | Organization description |
| logoUrl | String | No | Logo image URL |
| website | String | No | Website |
| email | String | Yes | Organization email |
| phone | String | No | Contact phone |
| address | String | No | Street address |
| city | String | No | City |
| state | String | No | State |
| zipCode | String | No | Postal code |
| country | String | No | Country |
| timezone | String | Yes | Organization timezone |
| primaryColor | String | No | Brand color |
| secondaryColor | String | No | Brand secondary color |
| isActive | Boolean | Yes | Active organization |
| createdBy | Document Reference | Yes | User who created the organization |
| createdAt | Timestamp | Yes | Creation date |
| updatedAt | Timestamp | Yes | Last update |

---

# Relationships

Organization

├── Users

├── Events

├── Speakers

├── Volunteers

├── Sponsors

├── Vendors

├── Announcements

└── Reports

---

# Used By

- Authentication
- Admin Dashboard
- Event Management
- Organization Settings

---

# Firestore Queries

## Get Organization

Filter

organizationId

---

## Active Organizations

Filter

isActive == true

---

## Search Organizations

Filter

organizationName

---

# CRUD Operations

Create

✔ Super Admin

Read

✔ Authenticated Users

Update

✔ Organization Admin

Delete

✔ Super Admin

---

# Security Rules

Read

Authenticated users belonging to the organization.

Write

Organization Admin

Delete

Super Admin only.

---

# Composite Indexes

organizationName ASC

isActive ASC

createdAt DESC

---

# Future Expansion

- Multiple campuses
- Departments
- Billing
- Subscription plans
- White-label branding
