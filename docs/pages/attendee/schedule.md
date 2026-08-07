# Schedule Page

## Overview

The Schedule Page displays all sessions for the selected event in chronological order.

Attendees can browse sessions, filter by track, room, speaker, or session type, and view detailed session information.

The Schedule Page is one of the most frequently used pages during an event.

---

# Purpose

Provide attendees with an organized and searchable agenda for the event.

---

# User Roles

- Attendee
- Speaker
- Volunteer (Read Only)
- Event Manager
- Organization Admin
- Super Admin

---

# Route

```
/attendee/schedule
```

---

# Navigation

Accessible From

- Home
- Bottom Navigation
- Session Details

Navigate To

- Session Details
- Speaker Profile
- Venue Details (Future)

---

# Firestore Collections

- events
- sessions
- tracks
- rooms
- speakers
- speakerAssignments

---

# Firestore Queries

## Current Event

events

status == Published

limit 1

---

## Sessions

sessions

eventRef == currentEvent

status == Published

orderBy startTime ASC

---

## Tracks

tracks

eventRef == currentEvent

status == Active

---

## Rooms

rooms

eventRef == currentEvent

status == Available

---

## Speaker Assignments

speakerAssignments

eventRef == currentEvent

status == Confirmed

---

## Speakers

speakers

status == Confirmed

---

# Components

- App Header
- Search Bar
- Filter Chips
- Date Selector
- Track Filter
- Session Card
- Bottom Navigation

---

# Actions

Search Sessions

↓

Filter List

---

Select Track

↓

Filter Sessions

---

Open Session

↓

Navigate to Session Details

---

Tap Speaker

↓

Navigate to Speaker Profile

---

Refresh

↓

Reload Queries

---

# Local State

| Variable | Type |
|----------|------|
| selectedDate | DateTime |
| selectedTrack | String |
| searchText | String |
| selectedRoom | String |

---

# App State

| Variable | Type |
|----------|------|
| currentEvent | Event |
| currentUser | User |

---

# Backend Actions

- Load Sessions
- Load Tracks
- Load Rooms
- Load Speakers

---

# Permissions

Authenticated users only.

---

# Loading State

Display skeleton Session Cards while loading.

---

# Empty State

"No sessions available."

---

# Error State

"Unable to load the event schedule."

---

# Success State

Schedule displayed successfully.

---

# Analytics Events

- Schedule Viewed
- Session Opened
- Track Filter Used
- Search Used

---

# Future Improvements

- My Schedule
- Calendar Sync
- AI Session Recommendations
- Live Session Updates
- Favorite Sessions
