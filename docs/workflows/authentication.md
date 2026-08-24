# Authentication Workflow

## Purpose

Define the complete authentication lifecycle for BEAM Event Hub using Firebase Authentication and the Firestore `users/{uid}` profile.

## Supported Flows

- Sign in
- Sign out
- Account registration
- Password reset
- Existing-session detection
- Account status validation
- Role-based routing

## Sign-In Flow

1. User opens the application.
2. Splash/authentication state check runs.
3. If no Firebase session exists, route to Login.
4. User enters email and password.
5. Validate required fields locally.
6. Authenticate with Firebase Authentication.
7. Read `users/{auth.uid}`.
8. If the user profile does not exist, stop the authenticated flow and send the account through profile/onboarding recovery rather than silently creating an incomplete record.
9. Check `status`.
10. If status is inactive, suspended, or otherwise blocked, deny application access and show the appropriate message.
11. Load role and organization context.
12. Route to the correct dashboard.

## Registration Flow

1. User selects Create Account.
2. Validate name, email, password, confirmation, and required terms.
3. Create Firebase Authentication account.
4. Obtain Firebase UID.
5. Create `users/{uid}` using that UID as the document ID.
6. Set default account status according to the approved registration policy.
7. Set default role to Attendee unless the user entered through an approved invitation/role-assignment workflow.
8. Store organization membership only when the organization relationship is authorized.
9. Mark profile completion state.
10. Route to onboarding or Attendee Home.

## Password Reset

1. User selects Forgot Password.
2. User enters email.
3. Validate email format.
4. Send Firebase password reset email.
5. Show a generic success message that does not disclose whether an account exists.

## Logout

1. User selects Logout.
2. Confirm if confirmation is required by the UX.
3. Sign out through Firebase Authentication.
4. Clear transient application state.
5. Navigate to Login and prevent authenticated pages from remaining accessible through navigation history.

## Session Handling

The app must use Firebase Authentication state as the authentication source of truth. Do not infer authentication from a Firestore user record alone.

At startup, check authentication state before protected queries are executed.

## Role Routing

After successful authentication, load the user's profile and determine the primary role.

| Role | Default destination |
|---|---|
| Super Admin | Super Admin Dashboard |
| Organization Admin | Organization Dashboard |
| Event Manager | Event Manager Dashboard |
| Volunteer | Volunteer Dashboard |
| Speaker | Speaker Dashboard |
| Attendee | Attendee Home |

If multiple roles exist, primary role determines the default destination while secondary permissions remain available where authorized.

## Error Handling

Handle at minimum:

- Invalid credentials
- Email already in use
- Weak password
- Invalid email
- Network unavailable
- Too many attempts / throttling
- Disabled account
- Missing user profile
- Permission denied
- Unknown/unexpected Firebase error

Messages should be understandable to users and must not expose sensitive backend details.

## Security Requirements

- Never store passwords in Firestore.
- Never trust client-side role visibility as authorization.
- Use Firestore Rules for protected data.
- Use the authenticated UID for ownership checks.
- Do not place Firebase service-account credentials in FlutterFlow or the repository.
- Do not expose internal permission details in user-facing errors.

## FlutterFlow Action Blueprint

### Login Button

Validate fields → Firebase Authentication: Log In → backend query `users` for current user → validate status → conditional role routing.

### Create Account Button

Validate form → Firebase Authentication: Create Account → Create Firestore User Document using authenticated UID → initialize profile → route to onboarding/home.

### Forgot Password

Validate email → Firebase Authentication password reset → confirmation state.

### Logout

Firebase Authentication: Log Out → Navigate to Login.

## Acceptance Criteria

- A valid user can sign in.
- Invalid credentials do not enter the app.
- A Firebase user without a valid application profile cannot access protected application data.
- Inactive/suspended users cannot access protected application pages.
- The correct dashboard opens based on primary role.
- Logout terminates the Firebase session.
- Password reset works without revealing account existence.
- Direct navigation cannot bypass backend authorization.
