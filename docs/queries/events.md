# Event Queries

## Published Events

Purpose: attendee event discovery.

Filters: publication status, registration/event visibility, organization/event scope, and date as needed.

Order: start date ascending for upcoming events.

## Current Event

Load the event selected by application context or the event configured as current/active.

## Admin Events

Scope by organization membership and required permissions. Support filters for status, date, and search fields.

## Event Detail

Load a single event by its document ID after verifying the user can access it.

## Rules

Never use a broad collection query and rely only on UI filtering for security. Query constraints should complement Firestore Rules.

## Required Indexes

Create composite indexes only when Firestore reports a required index for the final query combination. Record deployed indexes in the repository.
