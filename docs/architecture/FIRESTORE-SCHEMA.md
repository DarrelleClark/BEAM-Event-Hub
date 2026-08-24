# BEAM Event Hub — Firestore Schema

## 1. Identity Rule

Firebase Authentication owns authentication credentials. Cloud Firestore owns the application profile and business data.

The authoritative user document is:

```text
users/{firebaseAuthUid}
```

Never create a second random identifier for the primary user profile unless there is a documented business reason.

## 2. Core Collections

### organizations

Represents an organization using BEAM Event Hub.

Suggested fields:

- name: string
- slug: string
- description: string
- logoUrl: string
- websiteUrl: string
- status: string
- ownerRef: DocumentReference → users
- createdAt: Timestamp
- updatedAt: Timestamp

### users

Represents an authenticated application user.

Suggested fields:

- firstName: string
- lastName: string
- displayName: string
- email: string
- photoUrl: string
- primaryRole: string
- roles: array<string>
- primaryOrganization: DocumentReference → organizations
- organizations: array<DocumentReference>
- permissions: array<string>
- status: string
- profileComplete: boolean
- timezone: string
- language: string
- notificationPreferences: map
- createdAt: Timestamp
- updatedAt: Timestamp

### events

Represents an event managed by an organization.

Suggested fields:

- organizationRef: DocumentReference → organizations
- name: string
- slug: string
- description: string
- imageUrl: string
- status: string
- featured: boolean
- startDate: Timestamp
- endDate: Timestamp
- registrationOpen: Timestamp
- registrationClose: Timestamp
- venueRef: DocumentReference → venues
- createdBy: DocumentReference → users
- createdAt: Timestamp
- updatedAt: Timestamp

### venues

Represents a physical or virtual event venue.

Suggested fields:

- organizationRef: DocumentReference → organizations
- name: string
- address: string
- city: string
- state: string
- postalCode: string
- country: string
- mapUrl: string
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### rooms

Represents a room or event space within a venue.

Suggested fields:

- organizationRef: DocumentReference → organizations
- venueRef: DocumentReference → venues
- name: string
- description: string
- capacity: integer
- floor: string
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### tracks

Represents a category or track used to organize sessions.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- name: string
- description: string
- displayOrder: integer
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### sessions

Represents an individual event session.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- roomRef: DocumentReference → rooms
- trackRef: DocumentReference → tracks
- title: string
- description: string
- sessionType: string
- featured: boolean
- startTime: Timestamp
- endTime: Timestamp
- capacity: integer
- status: string
- materials: array<map>
- createdAt: Timestamp
- updatedAt: Timestamp

### speakers

Represents a speaker profile.

Suggested fields:

- organizationRef: DocumentReference → organizations
- userRef: DocumentReference → users, optional
- firstName: string
- lastName: string
- displayName: string
- title: string
- organizationName: string
- bio: string
- photoUrl: string
- websiteUrl: string
- featured: boolean
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### speakerAssignments

Connects speakers to sessions.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- sessionRef: DocumentReference → sessions
- speakerRef: DocumentReference → speakers
- role: string
- displayOrder: integer
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### registrations

Represents a user's registration for an event.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- userRef: DocumentReference → users
- registrationStatus: string
- registrationType: string
- registeredAt: Timestamp
- cancelledAt: Timestamp, optional
- createdAt: Timestamp
- updatedAt: Timestamp

A user should not have more than one active registration for the same event unless the business rules explicitly allow multiple registration records.

### tickets

Represents an attendee's event ticket/pass.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- userRef: DocumentReference → users
- registrationRef: DocumentReference → registrations
- ticketNumber: string
- qrValue: string
- ticketType: string
- status: string
- issuedAt: Timestamp
- expiresAt: Timestamp, optional
- createdAt: Timestamp
- updatedAt: Timestamp

### checkIns

Represents an attendee check-in transaction.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- userRef: DocumentReference → users
- registrationRef: DocumentReference → registrations
- ticketRef: DocumentReference → tickets
- checkedInAt: Timestamp
- checkedInBy: DocumentReference → users
- method: string
- status: string
- notes: string, optional

### announcements

Represents an event or organization announcement.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events, optional
- title: string
- body: string
- status: string
- priority: string
- featured: boolean
- publishAt: Timestamp
- expiresAt: Timestamp, optional
- createdBy: DocumentReference → users
- createdAt: Timestamp
- updatedAt: Timestamp

### sponsors

Represents an event sponsor.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- name: string
- logoUrl: string
- websiteUrl: string
- sponsorshipLevel: string
- description: string
- featured: boolean
- displayOrder: integer
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### vendors

Represents an event vendor.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- name: string
- description: string
- logoUrl: string
- boothName: string
- boothNumber: string
- contactName: string
- contactEmail: string
- status: string
- createdAt: Timestamp
- updatedAt: Timestamp

### volunteers

Represents volunteer assignments for an event.

Suggested fields:

- organizationRef: DocumentReference → organizations
- eventRef: DocumentReference → events
- userRef: DocumentReference → users
- role: string
- shiftStart: Timestamp
- shiftEnd: Timestamp
- location: string
- status: string
- notes: string, optional
- createdAt: Timestamp
- updatedAt: Timestamp

## 3. Reference Strategy

Use Firestore `DocumentReference` fields for parent/ownership relationships where FlutterFlow queries and security rules benefit from direct references.

Required ownership chain examples:

```text
event.organizationRef → organizations/{orgId}
session.eventRef → events/{eventId}
registration.userRef → users/{uid}
ticket.registrationRef → registrations/{registrationId}
checkIn.ticketRef → tickets/{ticketId}
```

## 4. Status Conventions

Use explicit status values rather than relying on missing fields.

Examples:

- active
- inactive
- draft
- published
- cancelled
- archived
- pending
- approved
- checked_in
- completed

Exact enum values should be standardized before production and used consistently in FlutterFlow, Firestore rules, queries, and reports.

## 5. Timestamps

Use Firestore Timestamp fields for dates and times. Prefer server timestamps when recording creation/update events.

## 6. Indexing

Composite indexes should be created when required by queries such as:

- events: `organizationRef + status + featured`
- sessions: `eventRef + featured + startTime`
- sessions: `eventRef + startTime`
- announcements: `eventRef + status + publishAt`
- sponsors: `eventRef + featured + displayOrder`
- registrations: `userRef + eventRef`
- tickets: `userRef + eventRef`
- speakerAssignments: `sessionRef + displayOrder`

Actual indexes should be generated from Firebase query errors and verified against production query patterns rather than created blindly.

## 7. Security Requirements

Every organization-owned document must be protected by organization membership.

Every user-owned registration and ticket must be protected by ownership rules.

Administrative writes must require the appropriate role or explicit permission.

Attendees must not be able to write administrative records such as events, sessions, speakers, sponsors, vendors, or check-ins unless a specific permission is granted.

## 8. Schema Change Policy

When changing a field or collection:

1. Update this document.
2. Update related query documentation.
3. Update FlutterFlow implementation documentation.
4. Update security rules.
5. Update QA cases.
6. Test existing workflows for regression.

The documentation and implementation must remain synchronized.
