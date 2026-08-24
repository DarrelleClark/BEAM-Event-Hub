# Registration Page

## Purpose

Collect required attendee registration information and submit an event registration.

## Flow

Event Details → Register → validate eligibility/status → collect required fields → duplicate check → Create Registration → ticket/pass creation → confirmation.

## Validation

Required fields must be complete; invalid values block submission. The button must show disabled/submitting state while the write is in progress.

## Errors

Registration closed, already registered, invalid data, permission denied, network failure, and ticket creation failure.

## Security

The authenticated UID is the registration owner. Users cannot choose another user ID through client-controlled fields.