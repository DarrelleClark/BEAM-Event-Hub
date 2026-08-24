# Volunteer Workflow

## Purpose

Define volunteer onboarding, event assignment, shift access, operational tasks, and check-in responsibilities.

## Volunteer Access

Volunteer access must be explicitly assigned to an organization/event. Being authenticated does not grant volunteer permissions.

## Assignment Flow

1. Authorized administrator creates/invites volunteer.
2. Volunteer account/profile is linked to the authenticated UID.
3. Volunteer is assigned to an organization/event.
4. Optional shift/task assignments are created.
5. Volunteer sees only assigned or authorized operational information.

## Volunteer Dashboard

Recommended sections:

- Current Event
- Shift Schedule
- Assigned Tasks
- Check-In
- Announcements
- Profile

## Check-In Responsibilities

Volunteers with `checkins.create` may perform check-in for their authorized event scope. The same ticket validation rules apply to volunteers as other authorized check-in staff.

## Shift Management

A shift should contain event, volunteer, start/end time, location/area, and status. Overlapping assignments should be detected before publication where practical.

## Restrictions

Volunteers cannot:

- Change their role or permissions.
- Modify organization membership.
- Publish events.
- Modify unrelated event data.
- Access another organization's data.

## Acceptance Criteria

- Volunteer sees only authorized assignments.
- Shift information is event-scoped.
- Check-in access is permission controlled.
- Volunteer cannot escalate privileges.
- Ended/inactive assignments no longer grant operational access where policy requires it.
