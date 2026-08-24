# Firestore Security Rules

## Purpose

Define the authorization contract that must be implemented in deployed Firestore Rules. This document is a specification; it is not proof that rules are currently deployed.

## Security Boundary

FlutterFlow visibility, navigation guards, and conditional widgets are not security controls. Firestore Rules must independently enforce access.

## Core Checks

Every protected operation should evaluate:

1. Authentication (`request.auth != null`).
2. User profile existence where application authorization requires it.
3. Account status.
4. Organization membership/scope.
5. Role and/or explicit permission.
6. Document ownership for user-owned data.
7. Valid write fields and immutable fields.

## Identity

Application profile: `users/{request.auth.uid}`.

Users may update only permitted profile fields on their own document. Role, permissions, organization membership, status, and other security-controlled fields require elevated authorization.

## Organization Isolation

Organization-scoped documents must not be readable or writable by users outside the owning organization. Child resources inherit the organization/event scope through their parent relationships or explicit organization metadata.

## Role/Permission Model

Use the documented roles and permission names as the application authorization vocabulary. Super Admin is platform-wide. Organization Admin, Event Manager, Volunteer, Speaker, and Attendee are scoped according to their documented permissions.

## Ownership

Attendee-owned registrations/tickets and personal data must be restricted to the authenticated owner unless an authorized staff permission permits access.

## Public Reads

Public access, if enabled, must be limited to intentionally public data such as published event/speaker content. Never make an entire collection public when only a subset of documents is public.

## Write Validation

Rules should reject writes that:

- Omit required fields.
- Change immutable ownership fields without permission.
- Change organization scope without permission.
- Grant roles or permissions without authorization.
- Modify another user's private data.
- Bypass lifecycle/status requirements.

## Soft Delete

Prefer status-based archival for business records that require historical reporting. Permanent deletion should be restricted and used only where policy permits.

## Audit Metadata

Where supported, protected business documents should maintain `createdAt`, `updatedAt`, `createdBy`, and `updatedBy`. Server/trusted timestamps are preferred for audit fields.

## Required Rule Tests

Before production, test every major collection with:

- Unauthenticated read/write
- Authenticated attendee access
- Attendee access to another attendee's data
- Volunteer scoped access
- Speaker scoped access
- Event Manager access
- Organization Admin access
- Super Admin access
- Cross-organization access
- Role/permission escalation attempts
- Invalid field/ownership updates

## Deployment Requirement

The project is not production-ready until actual Firestore Rules have been deployed to the intended Firebase project and automated/manual authorization tests pass.
