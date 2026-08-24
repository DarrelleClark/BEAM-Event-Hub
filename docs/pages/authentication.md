# Authentication Pages

## Login
Purpose: authenticate existing users.

Fields: email, password. Actions: Log In, Forgot Password, Create Account.

States: initial, validation error, authenticating, Firebase error, success.

Success action: load `users/{uid}`, validate status, then role-route.

## Account Registration
Fields: first name, last name, email, password, confirm password, required terms/consent.

Create Account remains disabled until required fields are valid and passwords match.

Success: Firebase account → `users/{uid}` → profile initialization → onboarding/home.

## Forgot Password
Email field → Firebase password-reset action → generic confirmation state.

## Splash / Auth Check
Show app branding while Firebase authentication state is resolved. Authenticated users proceed to profile/role routing; unauthenticated users go to Login.

## Security
Protected pages must require authentication and backend authorization. Do not expose role/permission controls to ordinary users.
