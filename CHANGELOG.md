# Changelog

## 1.3.1

- Fix trusting an app: a user decision now applies to that package and signing certificate, without changing the installer's verification status or trusting other apps from the same installer.
- Add removal of a user trust decision from app details, with English and Thai labels explaining what trust means.
- Refresh trust in the installed-app list and details, and omit personally trusted apps from the overview's unverified-app count. Installer filters continue to describe the installer, independently of user trust.
- Preserve active filters and sorting when a trust decision changes; refresh an open detail sheet with the current app data.
- Upgrade the local database from version 1 to 2 without destructive migration. Old decisions lack signing certificates and require confirmation again.
- Add regression tests for trust isolation, certificate changes, revocation, missing certificates, duplicate decisions, and database migration.

### Validation

See `DEVELOPMENT.md` for reproducible checks. A physical-device check remains required before publishing a release. This patch does not change the existing screen-sharing detection mechanism.

Local validation on Windows with JDK 21, 2026-10-25:

- `:app:assembleDebug`: passed; versionName 1.3.1, versionCode 29.
- `:app:testDebugUnitTest`: 40 tests passed, including 15 new regression tests and repository coverage on API 27 and API 36.
- `:app:lintDebug`: passed, with 22 warnings concerning dependency versions, the launcher vector, and resource shrinking.
- Recorded screenshots and visually reviewed the new trust controls at 360dp width.
- Merged debug manifest has no INTERNET permission.

![App details after a user trust decision on a 360dp-wide screen](image/v1.3.1-user-trust.png)
