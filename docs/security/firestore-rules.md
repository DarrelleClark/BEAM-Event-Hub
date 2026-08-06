# Firestore Security Rules

## Overview

BEAM Event Hub uses Firebase Authentication and Cloud Firestore Security Rules to protect application data.

Security is based on:

- Authentication
- Organization Membership
- User Roles
- Permissions
- Document Ownership

---

# Security Principles

- Every request must be authenticated.
- Users only access data for organizations they belong to.
- Users only perform actions they have permission to perform.
- Firestore Rules enforce security.
- FlutterFlow UI only improves user experience and must never be relied upon for security.

---

# Authentication

All requests require authentication unless explicitly marked public.

Example

request.auth != null

---

# Organization Isolation

Users may only access documents belonging to their organization.

Example

resource.data.organizationRef in user.organizations

---

# Role-Based Access

Permissions are evaluated using:

1. Super Admin
2. Primary Role
3. Secondary Roles
4. Individual Permissions

---

# Ownership

Users may edit their own profile.

Users may never edit another user's profile unless they have permission.

---

# Soft Delete

Collections should not be permanently deleted.

Instead:

status = "Archived"

---

# Public Collections

The following collections may allow public read access.

- Published Events
- Published Speakers
- Published Sponsors

Everything else requires authentication.

---

# Audit Fields

Every collection should contain:

createdAt

updatedAt

createdBy

updatedBy

---

# Required Metadata

Every secured collection should contain

organizationRef

createdAt

updatedAt

status

---

# Status Values

Draft

Published

Archived

Inactive

Active

Pending

Cancelled

Completed

---

# Validation Rules

All writes should validate:

- Required fields
- Data types
- Organization ownership
- User permissions

---

# Security Checklist

✓ Authentication required

✓ Organization verified

✓ Permission verified

✓ Required fields validated

✓ Metadata updated

✓ Audit trail maintained

---

# Future Enhancements

- Custom Claims
- Multi-Factor Authentication
- IP Restrictions
- API Keys
- Rate Limiting
- Audit Logs
- Security Monitoring
