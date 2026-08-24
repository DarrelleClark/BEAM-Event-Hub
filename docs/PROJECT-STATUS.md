# BEAM Event Hub — Project Status & Build Guide

## Source of Truth

Repository: `DarrelleClark/BEAM-Event-Hub`

Platform: FlutterFlow
Backend: Firebase
Database: Cloud Firestore
Authentication: Firebase Authentication
Storage: Firebase Storage
Notifications: Firebase Cloud Messaging

## 1. Repository Assessment

The repository is currently a product specification and implementation documentation repository. It contains architecture, collection definitions, security design, queries, workflows, page specifications, and component placeholders. It does not currently contain a complete exported FlutterFlow application or a complete Firebase deployment configuration.

The README identifies Authentication UI, Design System, Attendee Home, and Schedule as complete, with the Firestore repository in progress. Treat those as project-status claims until verified against the connected FlutterFlow and Firebase projects.

## 2. Functional Model

The documented application is organized around organizations, users, events, venues, rooms, tracks, sessions, speakers, speaker assignments, registrations, tickets, check-ins, announcements, sponsors, vendors, and volunteers.

Every authenticated account maps to a Firestore `users` document using the Firebase Authentication UID as the document ID.

## 3. Roles

Primary roles:

1. Super Admin
2. Organization Admin
3. Event Manager
4. Volunteer
5. Speaker
6. Attendee

A user may have a primary role plus secondary roles. The primary role controls default dashboard routing; effective permissions are derived from applicable roles and explicit permissions.

## 4. Authentication Target Architecture

### Login

1. App starts.
2. Authentication state is checked.
3. Unauthenticated users are sent to Login.
4. Login authenticates through Firebase Authentication.
5. The application loads `users/{auth.uid}`.
6. Account status is validated.
7. Primary role and organization membership are loaded.
8. The user is routed to the appropriate dashboard.

### Registration

1. User enters registration information.
2. Firebase Authentication creates the account.
3. The returned UID becomes the Firestore `users` document ID.
4. A user profile is created with required identity fields.
5. Role and organization assignment are applied according to the registration/invitation flow.
6. The user is routed to onboarding or the appropriate dashboard.

### Password Reset

Use Firebase Authentication's password reset flow. Passwords must never be stored in Firestore.

### Logout

Sign the user out of Firebase Authentication, clear appropriate application state, and return to Login.

## 5. Authorization

Authorization must be enforced by Firebase/Firestore rules, not only by FlutterFlow page visibility.

Required checks include authentication, account status, organization membership, organization ownership of requested documents, role/permission access, and ownership rules for profile-level data.

Super Admin has platform-wide access. Organization Admin is restricted to their organization. Event Manager is restricted to event-management responsibilities. Attendee, Speaker, and Volunteer have narrower operational access.

## 6. Firestore Identity Model

`users/{uid}` is the authoritative application profile record.

Core fields include firstName, lastName, displayName, email, primaryRole, roles, primaryOrganization, organizations, status, profileComplete, timezone, language, notification preferences, createdAt, and updatedAt.

## 7. Event Model

The event is the central parent record. Events connect to sessions, registrations, tickets, check-ins, speakers, speaker assignments, sponsors, vendors, volunteers, announcements, rooms, and tracks.

Typical lifecycle:

`Draft → Published → Registration Open → Registration Closed → In Progress → Completed`

Cancellation and archival are management states.

## 8. Build Sequence

### Phase 1 — Firebase Foundation

- Verify Firebase project.
- Enable Authentication.
- Enable Firestore.
- Enable Storage.
- Configure application settings and authorized domains.
- Configure FCM after core flows are stable.

### Phase 2 — Firestore Schema

Create and verify collections in this order:

1. organizations
2. users
3. events
4. venues
5. rooms
6. tracks
7. sessions
8. speakers
9. speakerAssignments
10. registrations
11. tickets
12. checkIns
13. announcements
14. sponsors
15. vendors
16. volunteers

### Phase 3 — Authentication

Build and verify Splash/auth check, Login, Registration, Forgot Password, Logout, user profile creation, role lookup, organization lookup, and role-based routing.

### Phase 4 — Attendee Experience

Build and verify Home, event details, Schedule, Session Details, Speaker Directory, Speaker Profile, Registration, QR Pass, Announcements, and Profile.

### Phase 5 — Operations

Build and verify Admin Dashboard, event management, venue/room management, tracks/sessions, speakers, speaker assignments, registrations, volunteers, check-in, announcements, and reporting.

### Phase 6 — Security

Before production, deploy and test Firestore Rules for authentication, organization isolation, role permissions, ownership, and archived records.

### Phase 7 — QA

Minimum end-to-end scenarios:

- New attendee registration
- Existing user login
- Invalid login
- Password reset
- Logout
- Role-based routing
- Organization isolation
- Event creation
- Session creation
- Speaker assignment
- Event registration
- Duplicate registration handling
- QR pass
- Check-in
- Announcement visibility
- Profile editing

## 9. Definition of Done

A feature is complete only when the UI exists, required Firestore fields exist, queries and actions are configured, loading/empty/error states are handled, backend permissions are enforced, valid and invalid cases have been tested, and documentation matches the implementation.

## 10. Security and Repository Rules

Do not commit Firebase service-account private keys, admin SDK credentials, production secrets, signing secrets, or passwords. Never store passwords in Firestore. UI visibility is not a security boundary.

## 11. Project Status Labels

Use these labels consistently:

- **Planned** — documented but not started.
- **In Progress** — currently being built.
- **Configured** — implementation exists but has not completed QA.
- **Tested** — valid and invalid cases verified.
- **Production Ready** — tested, secured, documented, and ready for deployment.

## 12. Current Priority

The highest-value checkpoint is:

`Login → Firebase Auth → users/{uid} → status/role/organization → role dashboard`

Once this identity flow is reliable, the rest of the application can build on a stable authorization model.
