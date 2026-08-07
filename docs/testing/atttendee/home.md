# Attendee Home Page - Quality Assurance Test Plan

## Overview

This document defines the quality assurance tests for the Attendee Home Page.

---

# Functional Tests

## Test 1

Scenario

User logs in successfully.

Expected Result

Attendee Home Page loads.

Status

Pending

---

## Test 2

Scenario

Current event exists.

Expected Result

Current Event Card displays correctly.

Status

Pending

---

## Test 3

Scenario

Featured sessions exist.

Expected Result

Featured Session Cards display.

Status

Pending

---

## Test 4

Scenario

Announcements exist.

Expected Result

Announcement cards display.

Status

Pending

---

## Test 5

Scenario

Sponsors exist.

Expected Result

Sponsor carousel loads.

Status

Pending

---

## Test 6

Scenario

User taps Schedule.

Expected Result

Navigate to Schedule Page.

Status

Pending

---

## Test 7

Scenario

User taps QR Pass.

Expected Result

QR Pass opens.

Status

Pending

---

## Test 8

Scenario

User taps Speaker.

Expected Result

Speaker Profile opens.

Status

Pending

---

# Firestore Tests

Current User Query

Pass

☐

Fail

☐

---

Current Event Query

Pass

☐

Fail

☐

---

Sessions Query

Pass

☐

Fail

☐

---

Announcements Query

Pass

☐

Fail

☐

---

Sponsors Query

Pass

☐

Fail

☐

---

Registration Query

Pass

☐

Fail

☐

---

Ticket Query

Pass

☐

Fail

☐

---

# UI Tests

☐ No overflow

☐ No clipping

☐ Responsive layout

☐ Images load

☐ Icons display

☐ Typography correct

☐ Theme colors correct

---

# Navigation Tests

☐ Home → Schedule

☐ Home → Session

☐ Home → Speaker

☐ Home → QR Pass

☐ Home → Notifications

☐ Home → Profile

---

# Empty State Tests

No Sessions

Expected

Display "No sessions available."

---

No Sponsors

Expected

Hide Sponsors section.

---

No Announcements

Expected

Hide Announcement section.

---

# Error Tests

Firestore Offline

Expected

Retry option appears.

---

Network Timeout

Expected

Loading indicator then error message.

---

Permission Denied

Expected

Access denied message.

---

# Security Tests

☐ User cannot access another attendee's data.

☐ User only sees published events.

☐ User only sees their own ticket.

☐ User only sees their own registration.

---

# Performance Tests

Home Page loads under 2 seconds.

Images lazy load.

Lists scroll smoothly.

No memory leaks.

---

# Accessibility Tests

Screen reader compatible.

Buttons have labels.

Color contrast meets WCAG AA.

Touch targets are at least 48x48dp.

---

# Regression Checklist

☐ Login still works.

☐ Schedule still loads.

☐ QR Pass still opens.

☐ Notifications still display.

☐ Session navigation still works.

☐ Speaker navigation still works.

---

# Test Status

| Test Area | Status |
|------------|--------|
| Functional | ☐ |
| UI | ☐ |
| Firestore | ☐ |
| Navigation | ☐ |
| Security | ☐ |
| Performance | ☐ |
| Accessibility | ☐ |

---

# Tester Notes

Date

Tester

Environment

Device

Operating System

FlutterFlow Version

Firebase Project

Notes

Issues Found

Recommendations
