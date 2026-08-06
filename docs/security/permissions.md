# BEAM Event Hub Permissions

## Overview

Permissions determine what actions a user may perform within BEAM Event Hub.

A user's permissions are evaluated after authentication and are independent of their primary role.

Roles provide a default set of permissions, while individual permissions allow additional access without changing the user's role.

---

# Permission Naming Convention

resource.action

Examples

events.read

events.create

events.update

events.delete

---

# Permission Categories

- Organizations
- Users
- Events
- Sessions
- Speakers
- Volunteers
- Vendors
- Sponsors
- Registrations
- Tickets
- Check-Ins
- Announcements
- Reports
- Settings

---

# Organization Permissions

| Permission | Description |
|------------|-------------|
| organizations.read | View organization information |
| organizations.create | Create organizations |
| organizations.update | Edit organization information |
| organizations.delete | Archive or delete organizations |

---

# User Permissions

| Permission | Description |
|------------|-------------|
| users.read | View users |
| users.create | Invite users |
| users.update | Edit users |
| users.delete | Archive users |
| users.roles | Assign user roles |
| users.permissions | Assign permissions |

---

# Event Permissions

| Permission | Description |
|------------|-------------|
| events.read | View events |
| events.create | Create events |
| events.update | Edit events |
| events.delete | Archive events |
| events.publish | Publish events |

---

# Session Permissions

| Permission | Description |
|------------|-------------|
| sessions.read | View sessions |
| sessions.create | Create sessions |
| sessions.update | Edit sessions |
| sessions.delete | Archive sessions |
| sessions.assignSpeakers | Assign speakers |

---

# Speaker Permissions

| Permission | Description |
|------------|-------------|
| speakers.read | View speakers |
| speakers.create | Create speakers |
| speakers.update | Edit speakers |
| speakers.delete | Archive speakers |

---

# Volunteer Permissions

| Permission | Description |
|------------|-------------|
| volunteers.read | View volunteers |
| volunteers.create | Create volunteers |
| volunteers.update | Edit volunteers |
| volunteers.delete | Archive volunteers |
| volunteers.assign | Assign volunteer shifts |

---

# Vendor Permissions

| Permission | Description |
|------------|-------------|
| vendors.read | View vendors |
| vendors.create | Create vendors |
| vendors.update | Edit vendors |
| vendors.delete | Archive vendors |

---

# Sponsor Permissions

| Permission | Description |
|------------|-------------|
| sponsors.read | View sponsors |
| sponsors.create | Create sponsors |
| sponsors.update | Edit sponsors |
| sponsors.delete | Archive sponsors |

---

# Registration Permissions

| Permission | Description |
|------------|-------------|
| registrations.read | View registrations |
| registrations.create | Register attendees |
| registrations.update | Update registrations |
| registrations.cancel | Cancel registrations |

---

# Ticket Permissions

| Permission | Description |
|------------|-------------|
| tickets.read | View tickets |
| tickets.create | Generate tickets |
| tickets.update | Edit tickets |
| tickets.invalidate | Invalidate tickets |

---

# Check-In Permissions

| Permission | Description |
|------------|-------------|
| checkins.read | View check-ins |
| checkins.create | Check attendees in |
| checkins.undo | Undo check-in |

---

# Announcement Permissions

| Permission | Description |
|------------|-------------|
| announcements.read | View announcements |
| announcements.create | Create announcements |
| announcements.update | Edit announcements |
| announcements.delete | Archive announcements |
| announcements.publish | Publish announcements |

---

# Report Permissions

| Permission | Description |
|------------|-------------|
| reports.read | View reports |
| reports.export | Export reports |
| reports.analytics | View analytics |

---

# Settings Permissions

| Permission | Description |
|------------|-------------|
| settings.read | View settings |
| settings.update | Update settings |

---

# Default Role Permissions

## Super Admin

Access to every permission.

---

## Organization Admin

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

## Event Manager

events.read

events.create

events.update

sessions.*

speakers.read

speakers.update

registrations.read

tickets.read

announcements.read

---

## Volunteer

checkins.read

checkins.create

registrations.read

tickets.read

announcements.read

---

## Speaker

sessions.read

speakers.read

announcements.read

---

## Attendee

events.read

sessions.read

speakers.read

announcements.read

tickets.read

registrations.read

checkins.read

---

# Best Practices

- Assign permissions rather than changing a user's role whenever possible.
- Archive users instead of deleting them.
- Use the principle of least privilege.
- Keep permission names consistent across the application.
- Use permissions to control UI visibility and backend authorization.
