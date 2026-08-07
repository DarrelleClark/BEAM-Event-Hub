# Attendee Home Page - FlutterFlow Implementation Guide

## Overview

This document describes how to implement the Attendee Home Page inside FlutterFlow.

This includes:

- Widget hierarchy
- Backend Queries
- Local State
- App State
- Actions
- Conditional Visibility
- Navigation
- Responsive Layout

---

# Page Information

Page Name

AttendeeHomePage

Route

/attendee/home

Authentication

Required

Primary Role

Attendee

---

# Theme

Primary Color

Deep Royal Purple (#4B2E83)

Secondary Color

White (#FFFFFF)

Accent

Metallic Gold (#E6C35E)

Typography

Headings

Playfair Display

Body

Montserrat

---

# Widget Tree

Scaffold

├── SafeArea

│

├── AppHeader

│

├── SingleChildScrollView

│

│ ├── WelcomeBanner

│

│ ├── CurrentEventCard

│

│ ├── QuickActionButtons

│

│ ├── FeaturedSessionsSection

│

│ ├── Today'sScheduleSection

│

│ ├── FeaturedSpeakersSection

│

│ ├── AnnouncementsSection

│

│ ├── SponsorsCarousel

│

│ └── Spacer

│

└── BottomNavigation

---

# Backend Queries

## Query 1

Current User

Collection

users

Filter

Document ID == auth.uid

Store As

currentUser

---

## Query 2

Current Event

Collection

events

Filter

status == Published

featured == true

Limit

1

Store As

currentEvent

---

## Query 3

Featured Sessions

Collection

sessions

Filter

eventRef == currentEvent

featured == true

Order By

startTime

---

## Query 4

Announcements

Collection

announcements

Filter

status == Published

Order By

publishAt DESC

Limit

5

---

## Query 5

Featured Speakers

Collection

speakers

Filter

featured == true

---

## Query 6

Sponsors

Collection

sponsors

Filter

featured == true

Order By

displayOrder

---

## Query 7

Current Registration

Collection

registrations

Filter

userRef == currentUser

eventRef == currentEvent

---

## Query 8

Current Ticket

Collection

tickets

Filter

userRef == currentUser

eventRef == currentEvent

---

# Components

| Component | Source |
|------------|--------|
| AppHeader | Reusable Component |
| CurrentEventCard | Reusable Component |
| SessionCard | Reusable Component |
| SpeakerCard | Reusable Component |
| SponsorCard | Reusable Component |
| AnnouncementCard | Reusable Component |
| BottomNavigation | Reusable Component |
| QuickActionButton | Reusable Component |

---

# Local State

| Variable | Type |
|------------|------|
| selectedSession | Document |
| selectedSpeaker | Document |
| selectedAnnouncement | Document |

---

# App State

| Variable | Type |
|------------|------|
| currentUser | Document |
| currentEvent | Document |
| currentOrganization | Document |
| currentRegistration | Document |
| currentTicket | Document |

---

# Actions

Page Load

↓

Load Current User

↓

Load Current Event

↓

Load Remaining Queries

↓

Display UI

---

Quick Action Buttons

Schedule

↓

Navigate

↓

SchedulePage

---

QR Pass

↓

Navigate

↓

QRPassPage

---

Session Card

↓

Navigate

↓

SessionDetailsPage

Parameter

sessionRef

---

Speaker Card

↓

Navigate

↓

SpeakerProfilePage

Parameter

speakerRef

---

Announcement

↓

Navigate

↓

AnnouncementDetailsPage

---

# Conditional Visibility

Current Event

Visible

Only if

currentEvent != null

---

Today's Sessions

Visible

Only if

sessions.count > 0

---

Announcements

Visible

Only if

announcements.count > 0

---

Sponsors

Visible

Only if

sponsors.count > 0

---

QR Button

Visible

Only if

registration exists

---

# Responsive Layout

Desktop

Maximum Width

1200px

Tablet

Maximum Width

900px

Mobile

Full Width

---

# Performance

Use Backend Pagination

Lazy Load Lists

Cache Images

Limit Featured Sessions

Limit Announcements

---

# Error Handling

Firestore Error

↓

Display SnackBar

↓

Retry Button

---

# Future Improvements

Offline Support

Realtime Updates

AI Recommendations

Live Event Banner

Networking Suggestions
