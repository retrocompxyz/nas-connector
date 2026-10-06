# Changelog

All notable changes to the NasConnector project.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [0.1.5] (build 2) — 2026-09-13

### Changed
- On launch and after the network connection is restored, the app now mounts
  **all saved shares** automatically, not only selected ones.
- Batch mounting is serialized so that overlapping triggers (launch + network
  event) do not skip shares.

### Removed
- The "Mount automatically at login" flag per share (column in the share list
  and option in the add/edit window).

## [0.1.4] (build 3) — 2026-09-13

### Fixed
- Mounting another share from the same server/IP failed
  ("Share not found" / Authentication error). The password is now passed
  correctly to `mount_smbfs` (in the URL, percent-encoded) and mounting forces
  a new session (`-s`).
- Detection of already-mounted shares — mounting is now idempotent.

### Changed
- Shares with a username/password are mounted via `/sbin/mount_smbfs` into
  `~/Mounts` (instead of NetFS).
- Guest shares (empty username) are mounted anonymously via NetFS into `/Volumes`.
- Added a NetFS fallback when `mount_smbfs` fails to mount a share.

### Added
- Mount operation logging to `~/Library/Logs/NasConnector/nasconnector.log`.
- Credential redaction in logs and error messages.

## [0.1.3] — 2026-09-13

### Changed
- Refactored the SMB mounting mechanism from NetFS to `/sbin/mount_smbfs`;
  shares with credentials go to `~/Mounts`.

### Added
- Guest share support via anonymous NetFS login.

## [0.1.2] — 2026-08-09

### Added
- First release: menu bar app, add/edit/delete SMB shares, passwords in Keychain,
  mounting via NetFS, mount at login, DMG package.
