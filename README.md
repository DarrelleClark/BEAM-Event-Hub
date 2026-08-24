# BEAM Event Hub

BEAM Event Hub is a modern event management platform built with FlutterFlow and Firebase.

## Technology Stack

- FlutterFlow
- Firebase Authentication
- Cloud Firestore
- Firebase Storage
- Firebase Cloud Messaging

## Documentation

The `docs/` directory is the project source of truth for architecture, data model, workflows, pages, reusable components, queries, security, QA, and implementation status.

Start here:

- [Documentation Hub](docs/README.md)
- [Project Status & Build Guide](docs/PROJECT-STATUS.md)
- [Project Roadmap](docs/PROJECT-ROADMAP.md)
- [Implementation Checklist](docs/IMPLEMENTATION-CHECKLIST.md)
- [Architecture](docs/architecture/ARCHITECTURE.md)
- [Firestore Schema](docs/architecture/FIRESTORE-SCHEMA.md)
- [Testing Strategy](docs/TESTING-STRATEGY.md)
- [Security Rules Specification](docs/security/firestore-rules.md)

## Core Modules

- Organizations
- Users and role-based access
- Events
- Venues and rooms
- Tracks and sessions
- Speakers and speaker assignments
- Registrations
- Tickets and QR passes
- Check-in
- Announcements
- Sponsors and vendors
- Volunteers
- Reports

## Project Status

The repository contains the product architecture and implementation documentation. Documentation may describe planned or target behavior; it does not by itself prove that the corresponding FlutterFlow/Firebase feature is deployed or tested.

Use the status labels in `docs/PROJECT-STATUS.md` and the checklist in `docs/IMPLEMENTATION-CHECKLIST.md` to distinguish Planned, In Progress, Configured, Tested, and Production Ready work.

## Security Notice

Firebase/Firestore authorization is a backend responsibility. FlutterFlow UI visibility is not a security boundary. Never commit passwords, Firebase service-account keys, production secrets, or signing credentials.
