# Registration Queries

## Current User Registration

Query registrations scoped by authenticated UID and selected event.

## Duplicate Check

Before creating a registration, query for an active registration matching the authenticated user and event.

## Admin Registration List

Authorized staff query registrations by event and permitted organization scope, with filters for status and check-in state.

## Registration Detail

Load a registration by ID only after authorization is established.

## Ticket Lookup

Resolve ticket/pass by its non-sensitive identifier for authorized check-in operations. Do not use private user data as the QR payload.

## Security

Attendees can read only their own registration/ticket data. Administrative reads require the appropriate permission and event/organization scope.
