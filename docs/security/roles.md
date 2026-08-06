# BEAM Event Hub Roles

## Overview

Roles determine a user's primary experience within BEAM Event Hub.

Each user has one **Primary Role** that determines:

- Default dashboard
- Navigation menu
- Landing page after login
- Default permissions

A user may also have multiple secondary roles, allowing additional permissions without changing their primary experience.

Example:

Primary Role

Organization Admin

Additional Roles

- Speaker
- Volunteer

---

# Role Hierarchy

```
Super Admin
    │
    ├── Organization Admin
    │       │
    │       ├── Event Manager
    │       │       │
    │       │       ├── Volunteer
    │       │       ├── Speaker
    │       │       └── Attendee
```

Higher roles inherit permissions from lower roles unless explicitly restricted.

---

# Super Admin

## Description

Platform owner.

Manages every organization within BEAM Event Hub.

---

## Dashboard

Platform Dashboard

---

## Responsibilities

- Create organizations
- Manage subscriptions
- Manage platform settings
- Manage all users
- Access every event
- View platform analytics
- Configure security

---

## Navigation

- Dashboard
- Organizations
- Users
- Events
- Reports
- Settings

---

## Default Permissions

organizations.*

users.*

events.*

sessions.*

speakers.*

volunteers.*

vendors.*

sponsors.*

registrations.*

tickets.*

checkins.*

announcements.*

reports.*

settings.*

---

# Organization Admin

## Description

Manages one organization and all events belonging to that organization.

---

## Dashboard

Organization Dashboard

---

## Responsibilities

- Manage organization
- Create events
- Invite users
- Manage volunteers
- Manage speakers
- Manage registrations
- Publish announcements

---

## Navigation

- Dashboard
- Events
- Sessions
- Speakers
- Volunteers
- Sponsors
- Vendors
- Registrations
- Reports
- Settings

---

## Default Permissions

organizations.read

organizations.update

users.read

users.create

users.update

events.*

sessions.*

speakers.*

volunteers.*

vendors.*

sponsors.*

registrations.*

tickets.*

checkins.*

announcements.*

reports.read

reports.export

settings.read

settings.update

---

# Event Manager

## Description

Responsible for planning and operating events.

---

## Dashboard

Event Dashboard

---

## Responsibilities

- Create events
- Manage sessions
- Manage schedules
- Assign speakers
- Manage registrations

---

## Navigation

- Dashboard
- Events
- Sessions
- Speakers
- Registrations
- Reports

---

## Default Permissions

events.read

events.create

events.update

sessions.*

speakers.read

speakers.update

registrations.*

tickets.read

announcements.read

reports.read

---

# Volunteer

## Description

Assists with event operations and attendee check-in.

---

## Dashboard

Volunteer Dashboard

---

## Responsibilities

- Check in attendees
- Verify tickets
- View assigned tasks
- View announcements

---

## Navigation

- Dashboard
- Check-In
- Assigned Tasks
- Announcements
- Profile

---

## Default Permissions

checkins.read

checkins.create

registrations.read

tickets.read

announcements.read

---

# Speaker

## Description

Presents one or more event sessions.

---

## Dashboard

Speaker Dashboard

---

## Responsibilities

- View assigned sessions
- Update speaker profile
- Upload presentation resources
- View event announcements

---

## Navigation

- Dashboard
- My Sessions
- Resources
- Profile

---

## Default Permissions

sessions.read

speakers.read

speakers.update

announcements.read

---

# Attendee

## Description

Registered participant attending an event.

---

## Dashboard

Attendee Home

---

## Responsibilities

- View schedule
- Register for sessions
- View speakers
- Receive announcements
- Display QR pass
- Check event information

---

## Navigation

- Home
- Schedule
- QR Pass
- Announcements
- Profile

---

## Default Permissions

events.read

sessions.read

speakers.read

announcements.read

registrations.read

tickets.read

checkins.read

---

# Multiple Roles

A user may belong to multiple roles.

Example

Primary Role

Organization Admin

Additional Roles

- Speaker
- Volunteer

The application always opens the dashboard associated with the Primary Role.

Permissions are calculated from all assigned roles plus any additional permissions.

---

# Permission Evaluation

Permissions are granted in this order:

1. Super Admin (Full Access)
2. Primary Role
3. Secondary Roles
4. Individual Permissions

The union of all permissions determines the user's effective access.

---

# Dashboard Routing

| Primary Role | Landing Page |
|---------------|--------------|
| Super Admin | Platform Dashboard |
| Organization Admin | Organization Dashboard |
| Event Manager | Event Dashboard |
| Volunteer | Volunteer Dashboard |
| Speaker | Speaker Dashboard |
| Attendee | Attendee Home |

---

# Future Roles

Potential future roles include:

- Sponsor Representative
- Vendor Representative
- Exhibitor
- Judge
- Mentor
- Moderator
- Photographer
- Media
- Parent
- Student Ambassador
- Sponsor Administrator

---

# Best Practices

- Every user must have exactly one Primary Role.
- Users may have multiple secondary roles.
- Roles determine navigation and dashboard routing.
- Permissions determine what actions a user can perform.
- Use individual permissions instead of creating unnecessary new roles.
- Grant the minimum permissions required to complete a user's responsibilities.
