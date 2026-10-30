# Changelog

All notable changes to Ocello. Versions follow [semantic versioning](https://semver.org).

## [3.2.0] – 2026-10-31

First public release.

### Security
- Every transfer is encrypted with TLS and pinned to each device's own key (P-256, created on first launch).
- Pairing shows a six-digit verification code on both screens; paired devices are remembered, and a device that copies a paired device's name is flagged.
- Pairing-code guessing is rate-limited (lockout after 10 wrong codes; the code changes after repeated guessing or a cancel).
- Session tokens are bound to the sender's address and expire after 5 idle minutes.
- One approval prompt at a time, with a cooldown after a decline; the prompt shows the sender's IP address.
- Received files can never be written outside the save folder, even through links.
- Programs, scripts and archives received on Windows carry the "downloaded from the internet" mark, so SmartScreen checks them.
- Android app data is excluded from cloud backup.

### Added
- Background transfers on Android with a progress notification and a Cancel button.
- Approval prompt with total size, item count, contents and free space.
- Cancel from the receiving device.
- Choose where received files are saved.
- Up to 16 parallel streams; large files are split across streams.

### Performance
- Small files travel in batches instead of one request each.
- Received data is written in 1 MB blocks; Android writes directly into Downloads.
- Encryption runs on several CPU cores, so it does not limit transfer speed.

### Changed
- New name (Ocello), logo and peacock-blue design.
- Odd file names are cleaned up instead of failing the transfer.

[3.2.0]: ../../releases/tag/v3.2.0
