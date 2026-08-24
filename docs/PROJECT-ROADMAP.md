# BEAM Event Hub — Project Roadmap

## Objective

Build a secure, role-based event platform that supports event administration, attendee registration, session discovery, speaker management, operational check-in, announcements, and event reporting.

## Phase 1 — Foundation

**Status: In Progress**

- Verify Firebase project connection
- Enable Firebase Authentication
- Enable Cloud Firestore
- Enable Firebase Storage
- Establish application environment settings
- Establish documentation and naming conventions

## Phase 2 — Data Model

**Status: In Progress**

Create and verify collections in this order:

1. `organizations`
2. `users`
3. `events`
4. `venues`
5. `rooms`
6. `tracks`
7. `sessions`
8. `speakers`
9. `speakerAssignments`
10. `registrations`
11. `tickets`
12. `checkIns`
13. `announcements`
14. `sponsors`
15. `vendors`
16. `volunteers`

## Phase 3 — Authentication

**Status: In Progress**

- Splash/auth-state check
- Login
- Account registration
- Forgot password
- Logout
- User document creation
- Account status validation
- Organization lookup
- Role and permission lookup
- Role-based dashboard routing

### Acceptance Criteria

A valid user can authenticate, the application resolves `users/{auth.uid}`, validates account status, identifies the organization and effective role, and routes the user to the correct dashboard. An invalid or inactive account cannot enter protected application areas.

## Phase 4 — Attendee Experience

**Status: Planned**

- Attendee Home
- Event details
- Schedule
- Session details
- Speaker directory
- Speaker profile
- Registration
- QR pass
- Announcements
- Profile

## Phase 5 — Event Operations

**Status: Planned**

- Organization management
- User management
- Event creation and editing
- Event publishing
- Venue management
- Room management
- Track management
- Session management
- Speaker management
- Speaker assignments
- Registration management
- Volunteer management
- Check-in
- Announcements
- Reporting

## Phase 6 — Security

**Status: Planned**

- Authentication rules
- Organization isolation
- Role-based permissions
- Document ownership rules
- User profile protection
- Registration ownership
- Ticket ownership
- Check-in authorization
- Archived-record restrictions

## Phase 7 — QA

**Status: Planned**

Test at minimum:

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
- Duplicate registration prevention
- QR pass
- Check-in
- Announcement visibility
- Profile editing
- Loading states
- Empty states
- Permission-denied states
- Network/firestore failures
- Responsive layouts
- Accessibility

## Phase 8 — Production Readiness

**Status: Planned**

- Security rules reviewed
- Indexes verified
- Error handling verified
- QA completed
- Analytics verified
- Storage rules reviewed
- Notifications tested
- Production environment confirmed
- Documentation reconciled with implementation
- Release checklist completed

## Current Critical Path

```text
Firebase Auth
   ↓
users/{uid}
   ↓
status
   ↓
organization membership
   ↓
role + permissions
   ↓
role dashboard
   ↓
protected application features
```

Do not move the project into production until this identity and authorization chain has been verified end-to-end.
