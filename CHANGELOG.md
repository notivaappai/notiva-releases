# Changelog

All notable changes to Notiva will be documented in this file.

The format is based on Keep a Changelog and follows Semantic Versioning.

# [1.0.1] - 2026-06-04

## Fixed

### Authentication
- Email verification flow no longer fails with `refresh_token required` when Supabase returns no refresh token after signup; app re-signs in with signup password when needed and only calls refresh when a refresh token exists.
- Empty auth tokens are no longer stored in the session.
- **Activate account** on login shows the correct message for already-verified emails (“This email is already verified. Please sign in.”) instead of the duplicate-account message.
- Auth error mapping checks `email_already_confirmed` before broad “already exists” patterns (client and backend).

### Password reset
- Forgot password uses the Go backend API only (no Supabase SDK/env in the Flutter app).
- Deep link recovery at opens the reset-password screen (cold start and warm link handling).
- Android intent filters updated for auth deep links.

### Notifications (Android release builds)
- Fixed release APK notification delivery (notification icon, manifest permissions).
- Clear separation between OS notification permission and in-app notification opt-in; “Skip for now” on onboarding no longer implies opt-in.
- Startup no longer auto-prompts for notification permission; settings reconcile on main navigation.

### UI / UX
- Dark mode: Add Transaction type toggle uses theme-aware colors (no hardcoded black).
- Forms no longer auto-open the keyboard on open (login, signup, forgot password, search, add task/transaction); tap outside to dismiss keyboard on major form screens.
- Dropdown menus on add task/transaction do not steal focus on tap.

## Added

### Authentication
- **Activate account** on login page: resend verification email and navigate to email verification screen.
- Backend `POST /v1/auth/resend-verification` with `404` when email not found and `409 email_already_confirmed` when already verified.

### Onboarding / navigation
- Onboarding and Welcome **Get Started** → Sign up; onboarding **Skip** → Log in.
- Initial setup: enabling notifications only after a real permission grant; skip does not opt in.

## Changed

- Signup passes password to the email verification page for post-verify sign-in fallback.

## Developer / ops notes

- Rebuild release APK/AAB after this version bump.

---

# [1.0.0] - 2026-06-02

## Initial Public Release

First public release of Notiva.

Notiva is an offline-first productivity and expense tracking application designed for ultra-fast data capture and secure Notion backup.

---

## Added

### Universal Quick Capture

Introduced natural language quick capture system.

Users can instantly create:

* Tasks
* Reminders
* Expenses
* Notes

Examples:

* Spent 250 on lunch
* Call Amit Monday
* Pay electricity bill tomorrow
* Buy groceries

---

### Task Management

Implemented task management system.

Features:

* Create tasks
* Update tasks
* Complete tasks
* Delete tasks
* Task status tracking

---

### Expense Tracking

Implemented transaction management.

Features:

* Income tracking
* Expense tracking
* Categories
* Payment methods
* Transaction history

---

### Smart Parsing Engine

Added rule-based NLP parser.

Capabilities:

* Intent detection
* Amount extraction
* Date extraction
* Category detection

Supported intents:

* Task
* Reminder
* Expense
* Note

---

### Offline First Architecture

Implemented local-first capture flow.

Features:

* Local storage persistence
* Offline capture support
* Sync queue
* Automatic retry

Users can continue using Notiva without internet connectivity.

---

### Local Capture Outbox

Added offline capture queue.

Features:

* Pending capture storage
* Automatic flush
* Background synchronization

---

### Budget Tracking

Implemented monthly budgeting system.

Features:

* Global monthly budget
* Budget consumption tracking
* Budget progress visualization

---

### Budget Alerts

Added over-budget detection.

Features:

* Monthly budget monitoring
* Threshold alerts
* Over-budget notifications

---

### Notifications

Implemented notification infrastructure.

Features:

* Reminder notifications
* Scheduled alerts
* Local notifications

---

### Priority Alert System

Added priority-based notification behavior.

Features:

* Priority levels
* Custom vibration patterns
* Alert differentiation

---

### Reminder Management

Implemented reminder workflow.

Features:

* Due dates
* Scheduled reminders
* Notification integration

---

### Dashboard

Implemented productivity dashboard.

Features:

* Task overview
* Expense overview
* Budget visibility
* Quick actions

---

### Transaction Filtering

Added transaction filtering capabilities.

Features:

* Date range selection
* Current month filtering
* Historical browsing

---

### Floating Action Button

Added global quick access entry point.

Features:

* Accessible from all tabs
* Launches Universal Quick Capture
* Instant data entry

---

### Notion Integration

Implemented secure Notion OAuth integration.

Features:

* Connect personal Notion workspace
* OAuth authentication
* Secure token storage
* Backend-managed integration

---

### Notion Backup System

Implemented one-way backup to Notion.

Features:

* Tasks backup
* Transactions backup
* Automatic database creation
* Template provisioning

---

### Notion Workspace Provisioning

Automatic workspace setup.

Creates:

* Notiva Tasks Database
* Notiva Transactions Database

inside the user's Notion workspace.

---

### Background Sync Engine

Implemented backend synchronization pipeline.

Features:

* Scheduled sync processing
* Retry support
* Failure tracking
* Sync status monitoring

---

### Secure Token Management

Implemented encrypted token storage.

Features:

* Token encryption at rest
* Backend-only access
* OAuth security protections

---

### Backend Architecture

Implemented production backend services.

Stack:

* Go
* PostgreSQL
* Supabase
* REST APIs

Features:

* Authentication
* Task APIs
* Transaction APIs
* Notion Integration APIs
* Sync Infrastructure

---

### Mobile Application

Implemented Flutter application.

Stack:

* Flutter
* Dart

Features:

* Cross-platform UI
* Offline support
* Responsive design
* Quick capture experience

---

### Authentication

Implemented secure authentication system.

Features:

* User accounts
* Session management
* Protected APIs

---

### Sync Reliability

Added synchronization safeguards.

Features:

* Retry mechanisms
* Sync status tracking
* Conflict prevention
* Error handling

---

## Security

### Notion OAuth

Implemented secure OAuth flow.

Features:

* OAuth state validation
* Encrypted token storage
* Backend-only token access

---

### API Security

Implemented:

* Protected endpoints
* User isolation
* Authorization checks

---

## Performance

### Capture Flow

Optimized capture speed.

Flow:

Capture
→ Local Save
→ Background Sync

Result:

Near-instant user experience.

---

### Offline Experience

Users can:

* Create tasks
* Create reminders
* Add expenses

without internet connectivity.

---

## 🛠 Developer Improvements

### Testing

Added parser test suite.

Coverage:

* Intent detection
* Amount extraction
* Date parsing
* Reminder parsing

---

### Code Quality

Verified:

* No analyzer issues in capture modules
* Stable synchronization pipeline
* Production-ready architecture

---

## Tech Stack

### Mobile

* Flutter
* Dart

### Backend

* Go
* PostgreSQL

### Infrastructure

* Supabase
* Notion API

### Authentication

* JWT
* OAuth 2.0

### Sync

* Background Workers
* Cron Jobs

---

## Core Features Available

* Universal Quick Capture
* Task Management
* Expense Tracking
* Budget Tracking
* Budget Alerts
* Notifications
* Reminder Management
* Offline First Support
* Automatic Sync
* Notion Backup
* Notion OAuth
* Transaction Filters
* Dashboard Analytics

---

## Planned

### Future Releases

* AI Powered Capture
* Smart Categorization
* Advanced Analytics
* Recurring Transactions
* Recurring Tasks
* Android Widgets
* Calendar Integration
* Export Features
* Team Workspaces
* iOS Support
* Play Store Release
