# QR Pass Card

Displays an event pass and QR identifier for an authorized attendee.

**Inputs:** ticket ID/status, event information, QR-safe identifier.

**Actions:** expand/open pass where supported.

**Security:** QR content must be a non-sensitive identifier; validation occurs server-side through authorized check-in workflows.

**States:** active, invalidated/cancelled, loading, unavailable.