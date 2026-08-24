# BEAM Event Hub Documentation

## Purpose

This directory is the source of truth for the BEAM Event Hub product architecture, data model, user experience, workflows, security model, implementation requirements, and quality assurance plan.

## Product

**BEAM Event Hub** is an event-management and attendee-engagement application for BEAM. The application is being built with FlutterFlow and Firebase.

### Technology Stack

- **Frontend:** FlutterFlow
- **Authentication:** Firebase Authentication
- **Database:** Cloud Firestore
- **File Storage:** Firebase Storage
- **Notifications:** Firebase Cloud Messaging

## Documentation Principles

1. Documentation describes the intended production behavior, not merely the current visual state.
2. Backend authorization is mandatory; FlutterFlow visibility is not a security boundary.
3. Firebase Authentication UID is the authoritative identity key for `users/{uid}`.
4. Organization ownership must be enforced consistently across organization-owned records.
5. Every feature must account for loading, empty, error, permission-denied, and success states.
6. A feature is not production-ready until its UI, data, actions, authorization, and QA requirements are documented and verified.

## Core Domain Model

The application is organized around:

- Organizations
- Users
- Events
- Venues
- Rooms
- Tracks
- Sessions
- Speakers
- Speaker Assignments
- Registrations
- Tickets
- Check-Ins
- Announcements
- Sponsors
- Vendors
- Volunteers

## User Roles

- Super Admin
- Organization Admin
- Event Manager
- Volunteer
- Speaker
- Attendee

A user may have a primary role and additional roles or explicit permissions.

## Implementation Order

1. Firebase foundation
2. Firestore schema
3. Authentication and account routing
4. Organization and user management
5. Event management
6. Venue, room, and track management
7. Session management
8. Speaker management and assignments
9. Attendee registration
10. Tickets and QR passes
11. Check-in
12. Announcements
13. Sponsor, vendor, and volunteer operations
14. Role-based dashboards
15. Security rules
16. End-to-end QA
17. Production readiness

## Key Identity Flow

```text
App Start
   ↓
Firebase Auth State
   ↓
Login / Registration
   ↓
Authenticated UID
   ↓
users/{uid}
   ↓
Account Status
   ↓
Organization Membership
   ↓
Primary Role / Permissions
   ↓
Role Dashboard
```

## Definition of Done

A feature is complete only when:

- The required UI exists.
- Required Firestore fields exist.
- Queries and actions are configured.
- Loading, empty, error, and permission states are handled.
- Backend permissions are enforced.
- Valid and invalid cases have been tested.
- Documentation matches the implementation.

## Documentation Map

| Area | Location |
|---|---|
| Project status | `docs/PROJECT-STATUS.md` |
| Product roadmap | `docs/PROJECT-ROADMAP.md` |
| Architecture | `docs/architecture/ARCHITECTURE.md` |
| Firestore model | `docs/architecture/FIRESTORE-SCHEMA.md` |
| Security | `docs/security/` |
| Workflows | `docs/workflows/` |
| Pages | `docs/pages/` |
| FlutterFlow implementation | `docs/flutterflow/` |
| Queries | `docs/queries/` |
| QA/testing | `docs/testing/` |
| Components | `docs/components/` |

## Status Labels

- **Planned:** documented but not started
- **In Progress:** actively being built
- **Configured:** implementation exists but has not completed QA
- **Tested:** valid and invalid cases verified
- **Production Ready:** tested, secured, documented, and ready for deployment
