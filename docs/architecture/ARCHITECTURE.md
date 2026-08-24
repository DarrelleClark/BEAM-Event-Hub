# BEAM Event Hub — System Architecture

## 1. Architecture Overview

BEAM Event Hub uses a FlutterFlow client backed by Firebase services.

```text
FlutterFlow Application
        │
        ├── Firebase Authentication
        │
        ├── Cloud Firestore
        │
        ├── Firebase Storage
        │
        └── Firebase Cloud Messaging
```

## 2. Client Layer

FlutterFlow provides:

- Pages and navigation
- Reusable components
- Forms and validation
- Backend queries
- Firestore create/read/update actions
- Conditional visibility
- Authentication actions
- Responsive layouts
- Role-based user experiences

Client-side visibility improves UX but does not provide security by itself.

## 3. Authentication Layer

Firebase Authentication is the identity provider.

The authenticated Firebase UID is the primary identity key for the application profile:

```text
users/{auth.uid}
```

Passwords are handled exclusively by Firebase Authentication and must never be stored in Firestore.

## 4. Application Identity

The `users/{uid}` document is the authoritative application profile.

Core identity data includes:

- firstName
- lastName
- displayName
- email
- primaryRole
- roles
- primaryOrganization
- organizations
- status
- profileComplete
- timezone
- language
- notification preferences
- createdAt
- updatedAt

## 5. Authorization Model

Authorization is based on four layers:

1. Authentication — is the user signed in?
2. Account status — is the account active and permitted to use the application?
3. Organization membership — does the user belong to the organization that owns the requested record?
4. Role/permission — is the user allowed to perform the requested operation?

Additional ownership checks apply to personal records such as registrations and tickets.

## 6. Roles

### Super Admin

Platform-wide administrative access.

### Organization Admin

Administrative access within the user's organization.

### Event Manager

Event-management access for assigned organizational responsibilities.

### Volunteer

Operational access focused on check-in and event support.

### Speaker

Access to speaker profile and assigned session information.

### Attendee

Access to published event information, registration, schedule, speakers, announcements, tickets, and personal profile data.

## 7. Domain Relationships

```text
Organization
   │
   ├── Users
   ├── Events
   │     ├── Venues / Rooms
   │     ├── Tracks
   │     ├── Sessions
   │     │     └── Speaker Assignments → Speakers
   │     ├── Registrations → Users
   │     ├── Tickets → Users
   │     ├── Check-Ins → Registrations / Users
   │     ├── Announcements
   │     ├── Sponsors
   │     ├── Vendors
   │     └── Volunteers
   │
   └── Organization-level settings
```

## 8. Event Lifecycle

The expected lifecycle is:

```text
Draft
  ↓
Published
  ↓
Registration Open
  ↓
Registration Closed
  ↓
In Progress
  ↓
Completed
```

Cancellation and archival are management states and must not be treated as normal attendee-facing lifecycle states.

## 9. Data Ownership

Organization-owned records must contain a reliable organization reference or otherwise be traceable to their owning organization.

Event-owned records must be traceable to their parent event.

User-owned records must be traceable to the authenticated user.

These relationships are required for both Firestore queries and security rules.

## 10. Storage

Firebase Storage is used for application files such as:

- User profile images
- Speaker profile images
- Event images
- Session materials
- Other approved event assets

Storage rules must enforce authentication, organization/event ownership where applicable, and appropriate upload/read permissions.

## 11. Notifications

Firebase Cloud Messaging is the target notification service.

Notifications should be introduced after authentication, core Firestore flows, and security rules are stable.

Potential notification categories include:

- Event announcements
- Session reminders
- Schedule changes
- Check-in information
- Administrative alerts

## 12. Query Design

Queries should be scoped as narrowly as practical using indexed fields such as:

- organizationRef
- eventRef
- userRef
- status
- featured
- startTime
- publishAt
- displayOrder

Avoid loading an entire collection when the UI only requires a filtered or limited subset.

## 13. Error Handling

Every important backend interaction must support:

- Loading state
- Empty state
- Success state
- Firestore/network error state
- Permission-denied state
- Retry behavior where appropriate

## 14. Performance

The application should:

- Limit list queries
- Paginate large datasets
- Lazy-load images and lists
- Avoid duplicate backend queries
- Use appropriate Firestore indexes
- Keep reusable components lightweight
- Avoid unnecessary global state

## 15. Production Boundary

The application is production-ready only when:

- Authentication is verified
- Firestore rules are deployed and tested
- Storage rules are deployed and tested
- Organization isolation is verified
- Role permissions are verified
- Critical workflows pass QA
- Error states are handled
- No production secrets are committed to the repository
- Documentation matches the deployed behavior
