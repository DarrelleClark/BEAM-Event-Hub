# Event Check-In Workflow

## Purpose

Provide authorized event staff with a fast, auditable method to validate a registration/ticket and record attendance.

## Roles

Check-in access is available only to authorized roles/permissions such as Super Admin, Organization Admin, Event Manager, and assigned Volunteer staff.

## QR Check-In Flow

1. Staff opens Check-In.
2. Selects the active event when necessary.
3. Scanner reads the ticket QR identifier.
4. App looks up the ticket/registration.
5. Validate that the ticket exists, belongs to the selected event, is active, and is associated with a valid registration.
6. Check whether the attendee is already checked in.
7. If valid and not checked in, create/update the check-in record.
8. Display attendee confirmation using only information staff are authorized to see.
9. Record timestamp and staff/user ID.

## Manual Check-In

When scanning is unavailable, authorized staff may search by an approved registration identifier or attendee information. Manual check-in must use the same validation rules as QR check-in.

## Duplicate Check-In

If the attendee is already checked in, do not create another active check-in. Show the existing check-in timestamp and staff information when permitted.

## Undo Check-In

Only users with `checkins.undo` may reverse a check-in. The reversal should preserve an audit trail rather than deleting historical evidence where possible.

## Offline/Failure Handling

The app must clearly distinguish between:

- Invalid ticket
- Ticket for another event
- Cancelled/invalidated ticket
- Already checked in
- Permission denied
- Network failure

Do not display a successful check-in until the write has succeeded or the application has an explicitly designed offline queue that is later reconciled.

## Security

- Check-in actions require authentication.
- Backend rules must enforce staff permissions.
- A volunteer can only check in within assigned/authorized event scope.
- Ticket identifiers must not expose private attendee information.
- Check-in records should contain event, registration/ticket, timestamp, and staff identity required for auditing.

## FlutterFlow Blueprint

Check-In Page → scan QR → query ticket/registration → conditional validation → Create Check-In → success/error state.

## Acceptance Criteria

- Valid ticket checks in successfully.
- Invalid/cancelled ticket is rejected.
- Ticket for another event is rejected.
- Duplicate check-in is prevented.
- Authorized staff can undo check-in when permitted.
- Unauthorized users cannot perform check-in writes.
- Check-in history remains auditable.
