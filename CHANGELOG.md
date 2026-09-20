# Changelog

All notable changes to **Notiva** are documented in this file.

The format is based on **Keep a Changelog**, and this project adheres to **Semantic Versioning (SemVer)**.

---
# [1.1.0] - 2026-09-20

## Summary

Adds five resizable Android home screen widgets for quick visibility into tasks, reminders, finances, and upcoming activity. Also improves task category filtering, widget navigation and privacy, and fixes the onboarding navigation flow.

## Highlights

- Added **five resizable Android widgets**.
- Added shared Flutter-to-Android widget data synchronization.
- Added widget deep links for tasks, calendar, transactions, and Quick Capture.
- Added privacy-aware financial amount masking.
- Improved task category selection and filtering.
- Fixed **Get Started → Sign Up → Sign In** navigation.
- Added widget documentation and automated tests.

## Added

### Android Widgets

Added five widgets:

- **Quick Overview** — tasks, spending, budget, priorities, and up-next activity.
- **Today's Focus** — priority-aware task list with up to 12 tasks.
- **Your Money** — financial statistics, budget progress, and recent transactions.
- **Quick Add** — shortcuts for creating reminders, transactions, and tasks.
- **Upcoming** — upcoming tasks and transactions grouped by priority.

All widgets support Android home screen resizing.

### Widget Synchronization

Added:

- `WidgetDataBuilder` for generating a shared application snapshot.
- `HomeWidgetSyncService` for debounced synchronization and widget refresh.
- Native Flutter-to-Android method-channel communication.
- Shared widget data storage using `SharedPreferences`.

Widget snapshots support signed-in and signed-out states and never contain authentication tokens.

### Widget Deep Links

Widgets can open:

- Tasks
- Calendar
- Transactions
- Quick Capture

### In-App Widget Components

Added reusable neumorphic widget components under:

```text
lib/views/widgets/home_widgets/
```

## Changed

### Task Categories

- Added category suggestions and type-to-filter chips.
- Improved category discovery and selection.
- Normalized category labels through `task_list_filter.dart`.

### Calendar

- Calendar can scroll directly to upcoming content when opened from a widget.

### Finance Privacy

- Widget financial amounts now respect the **Show Amounts** preference.

## Fixed

### Onboarding Navigation

Fixed an issue where **Onboarding → Sign Up → Sign In** could result in an empty black screen.

The authentication navigation now preserves the root route:

```text
Onboarding
    ↓
Get Started
    ↓
Sign Up
    ↓
Sign In
```

## Security & Privacy

- Authentication tokens are never stored in widget data.
- Widget data contains only information required for rendering.
- Financial amounts respect the user's visibility preference.
- Signed-out widget state does not expose session credentials.

## Performance

- Debounced widget data writes.
- Shared snapshot reduces duplicated processing.
- Native refreshes are triggered through the Flutter-to-Android bridge.
- Widgets render from persisted snapshot data.

## Compatibility

Existing Notiva functionality remains available, including:

- Quick Capture
- Task management
- Expense and budget tracking
- Reminders and notifications
- Offline-first capture
- Notion backup and synchronization
- Authentication

## Upgrade Notes

- Existing users can update without recreating their account.
- Android users can add widgets from the home screen widget picker.
- Widget content synchronizes from the Notiva application.
- Financial visibility follows the **Show Amounts** preference.

---

# [1.0.1] - 2026-06-04

## Summary

Maintenance release focused on authentication reliability, password recovery, notification behavior, and user experience improvements.

## Highlights

* Improved email verification and login reliability.
* Added **Activate Account** flow with verification email resend support.
* Fixed notification behavior in Android release builds.
* Enhanced form usability and onboarding experience.

## Added

### Authentication

* Added **Activate Account** option on the Login screen.
* Users can resend verification emails directly from the app.
* Added backend endpoint:

```http
POST /v1/auth/resend-verification
```

Response codes:

* `404` — Email not found.
* `409 email_already_confirmed` — Email already verified.

### Onboarding

* **Get Started** now navigates to **Sign Up**.
* **Skip** now navigates to **Log In**.
* Notification opt-in is enabled only after the user grants OS notification permission.

## Changed

### Authentication

* Signup now passes the user's password to the Email Verification screen, allowing automatic sign-in after successful verification when required.

## Improved

### User Experience

* Better onboarding flow.
* Improved keyboard behavior across forms.
* Improved dark mode appearance.
* Improved notification permission experience.

## Fixed

### Authentication

* Fixed email verification failing with `refresh_token required` when Supabase returned no refresh token after signup.
* Automatically signs users back in using their signup password when a refresh token is unavailable.
* Prevented empty authentication tokens from being stored.
* **Activate Account** now correctly shows:

  * "This email is already verified. Please sign in." for verified users.
  * Duplicate account errors only when appropriate.
* Improved authentication error mapping by checking `email_already_confirmed` before broader duplicate-account patterns.

### Password Recovery

* Forgot Password now uses the Go backend API exclusively.
* Recovery deep links correctly open the Reset Password screen during both cold and warm application launches.
* Updated Android intent filters for authentication deep links.

### Notifications

* Fixed notification delivery in Android release builds.
* Fixed notification icon configuration.
* Added required Android manifest permissions.
* Separated OS notification permission from in-app notification preferences.
* Choosing **Skip for now** during onboarding no longer enables notifications.
* Notification permission is no longer requested automatically during startup.
* Notification preferences are now synchronized after entering the main application.

### User Interface

* Fixed dark mode colors for the Add Transaction type selector.
* Prevented the keyboard from opening automatically on:

  * Login
  * Sign Up
  * Forgot Password
  * Search
  * Add Task
  * Add Transaction
* Added tap-outside-to-dismiss keyboard support across major forms.
* Prevented dropdown menus from stealing input focus.

## Security

* Prevented invalid or empty authentication tokens from being persisted in user sessions.

## Performance

* Reduced unnecessary startup work by delaying notification permission requests until appropriate.
* Improved authentication recovery flow by avoiding unnecessary token refresh attempts.

## Developer

### Internal Changes

* Rebuild release APK/AAB after upgrading to this version.

---

# [1.0.0] - 2026-06-02

## Summary

Initial public release of **Notiva**, an offline-first productivity and expense tracking application with secure Notion backup and background synchronization.

## Highlights

* Universal Quick Capture
* Offline-first architecture
* Task management
* Expense tracking
* Budget tracking
* Reminder notifications
* Secure Notion integration
* Background synchronization

## Added

### Universal Quick Capture

Create items using natural language.

Supports:

* Tasks
* Reminders
* Expenses
* Notes

Examples:

* Spent 250 on lunch
* Call Amit Monday
* Pay electricity bill tomorrow
* Buy groceries

### Task Management

* Create tasks
* Edit tasks
* Complete tasks
* Delete tasks
* Track task status

### Expense Tracking

* Income tracking
* Expense tracking
* Categories
* Payment methods
* Transaction history

### Smart Parsing Engine

Rule-based natural language parser supporting:

* Intent detection
* Amount extraction
* Date parsing
* Category detection

Supported intents:

* Task
* Reminder
* Expense
* Note

### Offline-First Architecture

* Local storage persistence.
* Offline data capture.
* Sync queue.
* Automatic retry.

### Local Capture Outbox

* Pending capture storage.
* Automatic queue processing.
* Background synchronization.

### Budget Tracking

* Monthly budget management.
* Budget consumption tracking.
* Budget progress visualization.

### Budget Alerts

* Monthly spending monitoring.
* Threshold alerts.
* Over-budget notifications.

### Notifications

* Reminder notifications.
* Scheduled alerts.
* Local notifications.

### Priority Alert System

* Priority-based reminders.
* Custom vibration patterns.
* Alert differentiation.

### Reminder Management

* Due dates.
* Scheduled reminders.
* Notification integration.

### Dashboard

* Task overview.
* Expense overview.
* Budget visibility.
* Quick actions.

### Transaction Filtering

* Date range filtering.
* Current month filtering.
* Historical browsing.

### Floating Action Button

* Available across all tabs.
* Launches Universal Quick Capture.
* Fast data entry.

### Notion Integration

* Secure OAuth authentication.
* Connect personal Notion workspace.
* Backend-managed integration.
* Secure token storage.

### Notion Backup

* One-way backup of:

  * Tasks
  * Transactions
* Automatic database creation.
* Template provisioning.

### Notion Workspace Provisioning

Automatically creates:

* Notiva Tasks Database
* Notiva Transactions Database

inside the connected Notion workspace.

### Background Synchronization

* Scheduled synchronization.
* Retry support.
* Failure tracking.
* Sync status monitoring.

### Backend Services

Built with:

* Go
* PostgreSQL
* Supabase

Includes:

* Authentication APIs
* Task APIs
* Transaction APIs
* Notion APIs
* Synchronization infrastructure

### Mobile Application

Built with:

* Flutter
* Dart

Features:

* Cross-platform UI
* Offline support
* Responsive design
* Universal Quick Capture

### Authentication

* User accounts.
* Session management.
* Protected APIs.

### Sync Reliability

* Retry mechanisms.
* Conflict prevention.
* Error handling.
* Sync status tracking.

## Changed

None.

## Improved

### Performance

* Optimized capture workflow using a local-first architecture for near-instant data entry.

### Offline Experience

Users can:

* Create tasks.
* Create reminders.
* Record expenses.

without an internet connection.

## Fixed

None.

## Security

### Notion OAuth

* OAuth state validation.
* Encrypted token storage.
* Backend-only token access.

### API Security

* Protected endpoints.
* User data isolation.
* Authorization enforcement.

## Performance

### Capture Flow

Optimized workflow:

```text
Capture
    ↓
Local Save
    ↓
Background Sync
```

Provides near-instant user experience while synchronizing data in the background.

## Developer

### Testing

Added parser test coverage for:

* Intent detection
* Amount extraction
* Date parsing
* Reminder parsing

### Code Quality

* Resolved analyzer issues in capture modules.
* Stabilized synchronization pipeline.
* Production-ready architecture.

### Technology Stack

| Layer           | Technology                    |
| --------------- | ----------------------------- |
| Mobile          | Flutter, Dart                 |
| Backend         | Go, PostgreSQL                |
| Infrastructure  | Supabase, Notion API          |
| Authentication  | JWT, OAuth 2.0                |
| Synchronization | Background Workers, Cron Jobs |

## Deprecated

None.

## Removed

None.

## Known Issues

None.

## Upgrade Notes

* Initial public release.

---

## Roadmap

Planned for future releases:

* AI-powered Quick Capture
* Smart categorization
* Advanced analytics
* Recurring tasks
* Recurring transactions
* Android widgets
* Calendar integration
* Export features
* Team workspaces
* iOS support
* Google Play Store release
