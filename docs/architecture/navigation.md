# Navigation Architecture

## Overview

The BEAM Event Hub application uses Role-Based Navigation.

Every authenticated user is directed to a dashboard based on their Primary Role.

Navigation is centralized and consistent throughout the application.

---

# Application Flow

Splash Screen

↓

Authentication Check

↓

Login

↓

Determine User Role

↓

Load Dashboard

---

# Role Routing

| Primary Role | Landing Page |
|--------------|--------------|
| Super Admin | Platform Dashboard |
| Organization Admin | Organization Dashboard |
| Event Manager | Event Dashboard |
| Volunteer | Volunteer Dashboard |
| Speaker | Speaker Dashboard |
| Attendee | Attendee Home |

---

# Navigation Structure

Authentication

├── Splash

├── Login

├── Register

└── Forgot Password

↓

Home

↓

Event

↓

Schedule

↓

Session

↓

Profile

---

# Public Pages

- Splash
- Login
- Register
- Forgot Password

---

# Protected Pages

- Home
- Schedule
- Sessions
- QR Pass
- Profile
- Notifications

---

# Admin Pages

- Dashboard
- Organizations
- Users
- Events
- Venues
- Rooms
- Tracks
- Sessions
- Speakers
- Sponsors
- Vendors
- Volunteers
- Reports
- Settings

---

# Attendee Pages

- Home
- Schedule
- Session Details
- Speaker Directory
- Speaker Profile
- QR Pass
- Notifications
- Profile

---

# Speaker Pages

- Speaker Dashboard
- My Sessions
- Session Details
- Resources
- Profile

---

# Volunteer Pages

- Volunteer Dashboard
- Check-In
- Shift
- Tasks
- Profile

---

# Event Manager Pages

- Dashboard
- Sessions
- Speakers
- Volunteers
- Registrations
- Reports

---

# Organization Admin Pages

- Dashboard
- Users
- Events
- Reports
- Sponsors
- Vendors
- Settings

---

# Navigation Rules

Unauthenticated users cannot access protected pages.

Users are redirected according to their Primary Role.

Users may switch organizations if they belong to multiple organizations.

Navigation menus are generated according to user permissions.

---

# Bottom Navigation

Attendee

- Home
- Schedule
- QR Pass
- Notifications
- Profile

Speaker

- Dashboard
- Sessions
- Resources
- Profile

Volunteer

- Dashboard
- Check-In
- Tasks
- Profile

---

# Future Navigation

- AI Assistant
- Networking
- Messages
- Marketplace
- Surveys
