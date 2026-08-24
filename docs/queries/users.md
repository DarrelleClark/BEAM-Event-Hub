# User Queries

## Current User

Primary query: `users/{auth.uid}`. This is the application profile lookup after Firebase authentication.

## Admin User Search

Search/filter users only within the administrator's authorized organization scope. Do not expose sensitive fields unnecessarily.

## Role/Permission Context

Read the current user's role/organization fields after authentication. Backend authorization remains authoritative.

## Profile Update

Update only fields explicitly allowed for the authenticated user. Security-controlled fields require elevated permission.

## Missing Profile

A valid Firebase account without a corresponding application user document must enter a controlled recovery/onboarding path rather than being treated as an authorized application user.
