# Session Queries

## Event Schedule

Query sessions where `eventId` equals the selected event and session visibility/status permits attendee access. Order by start time.

## Filters

Optional filters include day/date, track, room, speaker, and search text where supported.

## Session Detail

Load by session document ID after verifying event/user access.

## Speaker Sessions

Resolve sessions through `speakerAssignments` for an authorized speaker or through published session relationships for attendee views.

## Personal Schedule

If implemented, store only the attendee's authorized session selections and query by authenticated UID and event.
