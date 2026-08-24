# Event Registration Workflow

## Purpose

Define attendee registration from event discovery through registration, ticket creation, duplicate prevention, cancellation, and confirmation.

## Preconditions

- User is authenticated when registration requires an account.
- Event exists and is published.
- Registration is open.
- User is eligible for the event.

## Registration Flow

1. User opens an event.
2. App displays event details, registration status, dates, location, and eligibility information.
3. User selects Register.
4. App checks whether the user already has an active registration for the event.
5. If already registered, show the existing registration/ticket state instead of creating a duplicate.
6. Validate required registration fields.
7. Create the registration record with `userId`, `eventId`, status, timestamps, and any approved registration metadata.
8. Generate or associate a ticket/pass when the event requires one.
9. Display confirmation.
10. Make the registration available in the user's account and QR Pass experience.

## Registration Status

Recommended lifecycle:

`Pending → Confirmed → Checked In`

Cancellation may transition an active registration to `Cancelled`. No-show may be recorded after the event without destroying the original registration history.

## Duplicate Prevention

The application must prevent duplicate active registrations for the same user/event combination. This should be enforced in the workflow and, where practical, by data design/rules rather than relying only on UI state.

## Cancellation

1. User opens their registration.
2. Selects Cancel Registration.
3. Confirm intent.
4. Update registration status to Cancelled.
5. Invalidate an associated ticket when policy requires it.
6. Show confirmation.

## Ticket/QR Pass

A confirmed registration may have an associated ticket containing a non-sensitive unique identifier suitable for QR scanning. The QR value must not expose private user information.

## Admin Registration Management

Authorized staff can:

- Search registrations.
- Filter by event/status.
- View attendee details allowed by policy.
- Confirm or cancel registrations where permitted.
- Resend or regenerate ticket/pass artifacts where supported.
- Check an attendee in.
- Export approved registration data.

## Error States

Handle:

- Registration closed
- Event unpublished
- User not eligible
- Already registered
- Network failure
- Permission denied
- Ticket creation failure
- Event no longer available

## FlutterFlow Blueprint

Event Details → Register Button → duplicate-registration query → conditional form/confirmation → Create Registration → Create/associate Ticket → Success state.

## Acceptance Criteria

- User cannot create duplicate active registrations.
- Closed events cannot accept registrations.
- Registration records reference the correct authenticated user and event.
- Confirmation appears only after the database write succeeds.
- Ticket/QR pass is available when required.
- Cancellation updates state without destroying audit history.
