# Attendee Home Page

## Overview

The Attendee Home Page is the primary dashboard for attendees after signing in.

It provides quick access to event information, personalized content, schedules, announcements, speakers, sponsors, and the attendee's digital ticket.

This page is the central hub of the attendee experience.

---

# Purpose

Provide attendees with immediate access to everything they need during an event.

---

# User Roles

- Attendee

---

# Route

```
/attendee/home
```

---

# Navigation

Accessible From

- Login
- Bottom Navigation
- Notifications
- QR Pass
- Schedule

Navigate To

- Schedule
- Session Details
- Speaker Directory
- Speaker Profile
- QR Pass
- Notifications
- Profile
- Announcements

---

# Firestore Collections

- users
- events
- sessions
- speakers
- speakerAssignments
- announcements
- sponsors
- registrations
- tickets

---

# Firestore Queries

## Current User

users

Document ID = auth.uid

---

## Current Event

events

status == Published

featured == true

limit 1

---

## Featured Sessions

sessions

eventRef == currentEvent

featured == true

orderBy startTime

---

## Today's Sessions

sessions

eventRef == currentEvent

orderBy startTime

---

## Featured Speakers

speakers

featured == true

---

## Current Announcements

announcements

status == Published

orderBy publishAt DESC

limit 5

---

## Featured Sponsors

sponsors

featured == true

displayOrder ASC

---

## My Registration

registrations

userRef == currentUser

eventRef == currentEvent

---

## My Ticket

tickets

userRef == currentUser

eventRef == currentEvent

---

# Components

- App Header
- Welcome Banner
- Current Event Card
- Quick Action Buttons
- Featured Sessions
- Today's Schedule
- Featured Speakers
- Announcements
- Sponsors Carousel
- Bottom Navigation

---

# Actions

## View Schedule

Navigate to Schedule

---

## View Session

Open Session Details

---

## View Speaker

Open Speaker Profile

---

## Open QR Pass

Navigate to QR Pass

---

## Open Announcement

Navigate to Announcement Details

---

## View Sponsor

Open Sponsor Details

---

# Local State

| Variable | Type |
|----------|------|
| selectedAnnouncement | Announcement |
| selectedSession | Session |
| currentTab | Integer |

---

# App State

| Variable | Type |
|----------|------|
| currentUser | User |
| currentOrganization | Organization |
| currentEvent | Event |
| currentRegistration | Registration |
| currentTicket | Ticket |

---

# Backend Actions

- Load current user
- Load current event
- Load sessions
- Load announcements
- Load sponsors
- Load ticket
- Refresh page

---

# Permissions

Authenticated attendee only.

---

# Loading State

Display skeleton cards while loading.

---

# Empty State

If there are no upcoming sessions, display:

"No sessions have been scheduled yet."

---

# Error State

Display:

"Unable to load event information. Please try again."

---

# Success State

Dashboard loads successfully with current event information.

---

# Analytics Events

- Home Viewed
- Session Opened
- QR Pass Opened
- Speaker Opened
- Sponsor Viewed

---

# Future Improvements

- Personalized schedule
- AI recommendations
- Live announcements
- Networking suggestions
- Event countdown
- Weather widget
- Live polling
- Session reminders
