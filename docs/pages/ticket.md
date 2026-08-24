# Ticket / QR Pass Page

## Purpose

Display the authenticated attendee's active event pass and QR identifier.

## Data

Event, ticket status, registration status, approved display name, ticket identifier, and QR-safe value.

## Rules

Query only tickets owned by the authenticated user. Cancelled/invalidated tickets show a clear inactive state.

## QR Security

QR data must be a non-sensitive identifier. Check-in validation occurs against the backend ticket/registration record.

## States

Loading, active, pending, cancelled, invalidated, missing ticket, and error/retry.