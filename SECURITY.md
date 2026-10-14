# Security policy

## Supported versions

Only the latest release receives security fixes, on Windows and on Linux (Linux releases start with v0.7.0). The built-in updater offers new releases automatically; the `.deb` and `.rpm` packages are built without it and are updated by the package manager.

| Version | Windows | Linux |
|---------|---------|-------|
| Latest release | ✅ | ✅ |
| Older releases | ❌ | ❌ |

## Reporting a vulnerability

Please **do not** open a public issue. Report it privately through [Report a vulnerability](https://github.com/MouseDrive/MouseDrive/security/advisories/new) instead.

Include the MouseDrive version, the operating system, the steps to reproduce and what an attacker could achieve. You will get a first answer within 7 days. Once a fix is released, the advisory is published and you are credited unless you prefer otherwise.

## Scope

Of particular interest:

- The auto-updater on both systems: release lookup (including the HTTPS proxy settings and, on Linux, the system certificates), download, SHA-256 and minisign verification, the test run, self-replacement and rollback, and leaving package-manager installs alone.
- Windows: loading `vJoyInterface.dll` (search order, version matching).
- Linux: the udev rules and setup commands (`70-mousedrive.rules`, the optional `71-mousedrive-keyboard.rules`, the Setup window, the packages and the README). Their `uaccess` tag gives every program in the active local session access to `/dev/uinput` and to mice, and with the keyboard rule to every keystroke; a rule or command that grants more than the README describes is in scope.
- Linux: the virtual wheel on `/dev/uinput` and reading mice and keyboards through evdev.
- Reading and writing `config.toml` and profile files.

Bugs in the [vJoy driver](https://github.com/BrunnerInnovation/vJoy), in the Linux kernel's uinput and evdev drivers or in udev belong to those projects.
