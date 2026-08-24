# Administration Workflow

## Purpose

Define how authorized administrators manage organizations, users, events, content, registrations, and operational data.

## Access Model

Admin pages are permission protected. UI visibility is only a presentation layer; Firestore Rules enforce actual authorization.

## Admin Entry

1. Authenticate through Firebase.
2. Load `users/{uid}`.
3. Determine role and effective permissions.
4. Route to the appropriate management dashboard.
5. Load only organization/event data the administrator is authorized to access.

## Organization Management

Authorized administrators can create, view, update, and archive organizations according to their permissions. Organization identity and ownership must remain stable for related records.

## User Management

Admins can search users, view authorized profile information, invite users, assign roles, assign permissions, change account status, and archive accounts. Passwords are never managed in Firestore.

## Event Management

Event Managers and higher roles can:

- Create events.
- Edit event details.
- Configure registration windows.
- Publish/unpublish events.
- Archive events.
- Configure venue and room relationships.
- Manage tracks and sessions.
- Manage speakers and assignments.
- Review registrations.
- Publish announcements.

## Publishing Rules

An event should not be published until required event metadata and operational dependencies are present. The application should prevent incomplete events from being presented as public/active events.

## Registration Management

Authorized staff can search, filter, inspect, confirm/cancel where permitted, and support check-in operations. Destructive deletion should be avoided for records that are part of attendance history.

## Reporting

Reports should use approved, scoped queries and expose only information permitted by the current organization/event context. Exports require explicit report/export permission.

## Audit Expectations

Important administrative actions should retain timestamps and actor identity where supported, especially:

- Role/permission changes
- Account status changes
- Event publication
- Registration status changes
- Ticket invalidation
- Check-in reversal
- Announcement publication

## Acceptance Criteria

- Unauthorized users cannot access admin writes.
- Organization isolation is enforced.
- Admin lists support loading, empty, and error states.
- Publishing cannot bypass required data validation.
- Archived records remain auditable.
- Sensitive information is never exposed beyond the administrator's scope.
