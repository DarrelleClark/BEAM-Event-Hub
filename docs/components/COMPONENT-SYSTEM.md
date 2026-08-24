# BEAM Event Hub Component System

All reusable components should be implemented as FlutterFlow Components where reuse and consistent behavior are beneficial.

## Shared Rules

- Use the design system typography/spacing/radius definitions.
- Expose only necessary component parameters.
- Keep navigation/actions configurable rather than hard-coded where practical.
- Define loading, empty, disabled, and error states where relevant.
- Never put authorization decisions solely inside a component.

## Components

### App Header
Displays page title/context, navigation affordances, notifications, and profile access.

### Bottom Navigation
Primary attendee navigation. Selected state must reflect the current route and inaccessible destinations must not be shown.

### Event Card
Shows event image/title/date/location/status and opens Event Details.

### Session Card
Shows title/time/room/track/speaker summary and opens Session Details.

### Speaker Card
Shows approved speaker photo/name/title and opens Speaker Profile.

### Sponsor Card
Shows approved sponsor branding/content and opens approved destination.

### Announcement Card
Shows title/message/date and opens announcement details when a detail view exists.

### Venue Card
Shows venue/location information and opens venue details where supported.

### Ticket/QR Pass Card
Shows ticket status and QR identifier. Never encode private profile data in the QR payload.

### Quick Action Button
Reusable icon/label action for Home shortcuts. Supports enabled/disabled states and navigation/action callbacks.

### Section Header
Reusable section title with optional action link.

## Component QA

Every component should be tested with normal data, missing optional data, long text, loading/error state where relevant, narrow screen width, and unauthorized/disabled action state.
