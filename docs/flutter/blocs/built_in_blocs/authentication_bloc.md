---
title: AuthenticationBloc
sidebar_position: 1
---

# AuthenticationBloc

The `AuthenticationBloc` is responsible for managing the entire authentication flow in the Supa Flutter app. It handles authentication states, login/logout events, user session persistence, and multi-tenant support across various identity providers (Google, Apple, Microsoft, Password, and Biometrics).

---

## 🧠 Responsibilities

- Manages login state transitions across multiple identity providers.
- Handles multi-tenant and tenant-selection logic.
- Persists authentication state (via `authRepo.saveAuthentication`).
- Emits loading, error, and authenticated states.
- Integrates with external platforms like Azure AD and Google OAuth.

---

## 🎯 Use Cases

- Login with password or social accounts
- Automatic login with biometrics or saved credentials
- Select tenant from multiple available ones
- Update user profile preferences (email/notification)
- Logout and clear session
- Handle authentication errors gracefully

---

## ⚙️ Initialization

```dart
final bloc = AuthenticationBloc();
bloc.handleInitialize();
```

This triggers a check for saved credentials or shows the login screen.

---

## 🔁 State Transitions

| State                                      | Description                                      |
|-------------------------------------------|--------------------------------------------------|
| `AuthenticationInitialState`              | Initial state before any action is taken         |
| `AuthenticationProcessingState`           | Emitted during any login operation               |
| `UserAuthenticatedWithSelectedTenantState`| Authenticated with a chosen tenant               |
| `UserAuthenticatedWithMultipleTenantsState`| Authenticated, tenant selection pending         |
| `AuthenticationErrorState`                | Error during login or profile update             |
| `AuthenticationLogoutState`               | Logged out and reset to initial state            |

---

## 🧩 Events

### Login Events

| Event                                | Description                         |
|-------------------------------------|-------------------------------------|
| `LoginWithGoogleEvent`              | Google sign-in via OAuth            |
| `LoginWithAppleEvent`               | Apple ID sign-in                    |
| `LoginWithMicrosoftEvent`          | Azure AD sign-in                    |
| `LoginWithPasswordEvent(email, password)` | Manual login via email/password |
| `LoginWithSavedLoginEvent`          | Auto-login with biometrics/saved credentials |

### Session & State

| Event                                  | Description                        |
|---------------------------------------|------------------------------------|
| `AuthenticationInitializeEvent`       | Reset auth to initial state        |
| `UsingSavedAuthenticationEvent`       | Load and reuse saved credentials   |
| `AuthenticationProcessingEvent`       | Trigger loading state              |
| `AuthenticationErrorEvent`            | Report and handle errors           |
| `UserLogoutEvent`                     | Logout and clear session           |

### Multi-Tenant Support

| Event                                   | Description                        |
|----------------------------------------|------------------------------------|
| `LoginWithSelectedTenantEvent(tenant)` | Select tenant to finalize login    |
| `LoginWithMultipleTenantsEvent`        | Show tenant selector UI            |

### User Profile Management

| Event                                      | Description                     |
|-------------------------------------------|---------------------------------|
| `UpdateAppUserProfileEvent(user)`         | Update stored profile           |
| `AppUserSwitchEmailEvent`                 | Toggle email notifications      |
| `AppUserSwitchNotificationEvent`          | Toggle in-app notifications     |

---

## 🧠 State Properties

```dart
state.isAuthenticated       // true if logged in with selected tenant
state.isSelectingTenant     // true if multiple tenants detected
state.isLoading             // true if any login is in progress
state.hasError              // true if current state is an error
```

---

## 🎛 Azure AD Configuration

```dart
oauth = bloc.configureAzureAD(navigatorKey, redirectUri);
```

Sets up the Azure AD client using `aad_oauth`. Called before `LoginWithMicrosoftEvent`.

---

## 🧠 Best Practices

- Always wrap login events with `AuthenticationProcessingEvent(...)` for consistent UX.
- Use `handleLoginWithTenants(...)` for tenant-aware logins.
- Catch errors and emit `AuthenticationErrorEvent` to display user-friendly feedback.
- Use `handleInitialize()` at app launch to restore saved sessions.

---

## 📂 File Structure

```txt
lib/blocs/authentication/
  ├── authentication_bloc.dart
  ├── authentication_event.dart
  ├── authentication_state.dart
  └── authentication_action.dart
```
