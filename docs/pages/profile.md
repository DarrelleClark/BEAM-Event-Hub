# Profile Page

## Purpose

Allow users to view and edit profile fields permitted by their role.

## Display

Name, email, profile photo, role/read-only organization context, timezone, language, notification preferences, and profile completion state.

## Editable Fields

Only approved profile fields may be edited. Role, permissions, account status, organization membership, and other security-controlled fields are not editable by ordinary users.

## Actions

Save changes, change profile photo where enabled, notification preferences, and Logout.

## Validation

Validate required names and allowed field lengths/formats. Show unsaved-change and save-success/error states.

## Security

Update only `users/{auth.uid}` fields explicitly allowed by backend rules.
