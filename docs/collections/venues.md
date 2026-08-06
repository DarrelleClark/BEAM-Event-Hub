# Venues Collection

## Overview

The `venues` collection stores physical locations where events are held.

A venue may host multiple events over time and contains one or more rooms where sessions and activities take place.

Examples include convention centers, schools, hotels, community centers, and university campuses.

---

# Firestore Collection

venues

---

# Purpose

The Venues collection centralizes all location information used throughout the application.

It provides:

- Venue information
- Maps
- Addresses
- Parking details
- Accessibility information
- Room management

---

# Document ID Strategy

Firestore Auto ID

Example

venue_01

---

# Venue Types

Supported values

- Convention Center
- Hotel
- University
- School
- Community Center
- Corporate Office
- Outdoor Venue
- Virtual
- Hybrid

---

# Fields

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| organizationRef | Document Reference | Yes | Organization that owns the venue |
| venueName | String | Yes | Venue name |
| venueType | String | Yes | Venue type |
| description | String | No | Description |
| imageUrl | String | No | Cover image |
| addressLine1 | String | Yes | Street address |
| addressLine2 | String | No | Suite or building |
| city | String | Yes | City |
| state | String | Yes | State or province |
| postalCode | String | Yes | ZIP or postal code |
| country | String | Yes | Country |
| latitude | Double | No | GPS latitude |
| longitude | Double | No | GPS longitude |
| phone | String | No | Venue phone |
| email | String | No | Venue email |
| website | String | No | Website |
| parkingAvailable | Boolean | Yes | Parking available |
| parkingDetails | String | No | Parking instructions |
| accessible | Boolean | Yes | ADA accessible |
| wifiAvailable | Boolean | Yes | Public Wi-Fi |
| emergencyContact | String | No | Emergency contact |
| status | String | Yes | Active, Inactive, Archived |
| createdBy | Document Reference | Yes | Creator |
| createdAt | Timestamp | Yes | Creation date |
| updatedBy | Document Reference | No | Last updated by |
| updatedAt | Timestamp | Yes | Last update |

---

# Status

Allowed values

- Active
- Inactive
- Archived

---

# Relationships

Venue

├── Rooms

└── Events

---

# Business Rules

- Every venue belongs to one organization.
- One venue may host many events.
- A venue may contain multiple rooms.
- Latitude and longitude should be provided for maps.
- Archived venues cannot be assigned to new events.

---

# Validation Rules

- Venue name is required.
- Address is required.
- City is required.
- State is required.
- Country is required.
- Organization reference is required.

---

# Security Rules

## Read

Authenticated users

Organization staff

Super Admin

---

## Create

Organization Admin

Super Admin

---

## Update

Organization Admin

Super Admin

---

## Delete

Super Admin

Recommendation:

Archive venues instead of deleting.

---

# Firestore Queries

## Active Venues

status == "Active"

---

## Venues by Organization

organizationRef == currentOrganization

---

## Search Venues

venueName

city

state

---

# Composite Indexes

organizationRef ASC

status ASC

venueName ASC

city ASC

---

# CRUD Operations

| Operation | Attendee | Speaker | Volunteer | Event Manager | Organization Admin | Super Admin |
|------------|----------|----------|------------|---------------|--------------------|-------------|
| Create | No | No | No | No | Yes | Yes |
| Read | Yes | Yes | Yes | Yes | Yes | Yes |
| Update | No | No | No | No | Yes | Yes |
| Delete | No | No | No | No | Archive | Yes |

---

# Used By

- Home
- Event Details
- Venue Page
- Schedule
- Session Details
- Admin Dashboard

---

# Example Document

```json
{
  "organizationRef": "/organizations/beam",
  "venueName": "Oregon Convention Center",
  "venueType": "Convention Center",
  "description": "Primary venue for the Black Student Success Summit.",
  "imageUrl": "",
  "addressLine1": "777 NE Martin Luther King Jr Blvd",
  "addressLine2": "",
  "city": "Portland",
  "state": "Oregon",
  "postalCode": "97232",
  "country": "USA",
  "latitude": 45.5285,
  "longitude": -122.6632,
  "phone": "+1-503-235-7575",
  "email": "info@examplevenue.org",
  "website": "https://examplevenue.org",
  "parkingAvailable": true,
  "parkingDetails": "Parking garage available on Level P1.",
  "accessible": true,
  "wifiAvailable": true,
  "emergencyContact": "+1-503-555-0100",
  "status": "Active",
  "createdBy": "/users/uid123",
  "createdAt": "2026-08-01T12:00:00Z",
  "updatedBy": "/users/uid123",
  "updatedAt": "2026-08-06T12:00:00Z"
}
```

---

# Future Enhancements

- Interactive maps
- Indoor navigation
- Room occupancy
- Parking lot maps
- EV charging locations
- Public transportation links
- Nearby hotels
- Nearby restaurants
- Weather integration
- Geofencing for check-in
