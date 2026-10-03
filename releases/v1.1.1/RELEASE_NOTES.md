## Summary

Adds user-configurable transaction period settings (optional period start date and day-of-month anchor) so month/year/custom ranges follow a billing cycle instead of calendar month boundaries or fixed rolling windows. Wires the same settings through transactions, tasks, home widgets, and persisted finance settings.

## Highlights

- Added **transaction period configuration** with period start date & day-of-month anchor (e.g., 15th).
- Replaced inline UI with shared `TransactionDateFilterBar` widget for period chips & custom range picking.
- Syncs period settings across Transactions, Tasks, Home Widgets, and Finance Settings.
- Added global notifiers (`transactionPeriodStartNotifier`, `transactionPeriodDayNotifier`) for real-time updates.
- Android build now runs without `key.properties` (avoids CI failures).

## Full changelog
https://github.com/notivaappai/notiva-releases/blob/main/CHANGELOG.md#110---2026-09-20