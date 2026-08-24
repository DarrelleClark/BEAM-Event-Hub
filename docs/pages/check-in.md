# Check-In Page

## Purpose

Provide authorized event staff with QR scanning and manual attendee check-in.

## Flow

Select event → scan/search ticket → validate event/ticket/registration → check duplicate state → create check-in → show success.

## Staff Scope

Check-in writes require explicit permission and event/organization scope.

## States

Scanner ready, processing, valid, already checked in, invalid ticket, wrong event, cancelled ticket, permission denied, offline/error.

## Audit

Check-in records should preserve event, registration/ticket, timestamp, and staff actor information.