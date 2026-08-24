# Attendee Home Page

## Purpose

Primary landing page for authenticated attendees.

## Data

Load current/published event context, featured sessions, published announcements, approved sponsor content, and the current user's registration/ticket state where applicable.

## Sections

1. Header/greeting
2. Current Event Card
3. Featured Sessions
4. Announcements
5. Sponsors (optional)
6. Quick Actions: Schedule, QR Pass, Speakers, Notifications

## Navigation

Schedule → Schedule Page
Session card → Session Details
Speaker → Speaker Profile
QR Pass → Ticket/QR Pass
Notifications → Announcements
Profile → Profile

## States

Loading skeleton; empty event state; no sessions; no announcements; offline/error retry; permission denied.

## Acceptance Criteria

Only published and authorized data appears. All navigation targets resolve correctly. The page does not expose another user's registration/ticket.
