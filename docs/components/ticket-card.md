# Ticket Card

Displays the user's authorized ticket/pass summary: event, ticket status, attendee-approved display name, and QR/pass action.

**Security:** query only the authenticated user's authorized ticket. Do not place private profile data inside the QR payload.

**Actions:** open QR Pass; show invalid/cancelled state.

**States:** active, pending, cancelled, invalidated, loading, error.