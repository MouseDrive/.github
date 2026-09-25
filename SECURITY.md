# Security policy

## Supported versions

Only the latest release receives security fixes. The built-in updater offers new releases automatically.

| Version | Supported |
|---------|-----------|
| Latest release | ✅ |
| Older releases | ❌ |

## Reporting a vulnerability

Please **do not** open a public issue. Report it privately through [Report a vulnerability](https://github.com/MouseDrive/MouseDrive/security/advisories/new) instead.

Include the MouseDrive version, the steps to reproduce and what an attacker could achieve. You will get a first answer within 7 days. Once a fix is released, the advisory is published and you are credited unless you prefer otherwise.

## Scope

Of particular interest:

- The auto-updater: release lookup, download, SHA-256 verification and self-replacement.
- Loading `vJoyInterface.dll` (search order, version matching).
- Reading and writing `config.toml` and profile files.

Bugs in the vJoy driver itself belong to the [vJoy project](https://github.com/BrunnerInnovation/vJoy).
