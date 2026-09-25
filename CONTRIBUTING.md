# Contributing to MouseDrive

Thanks for your interest in MouseDrive! Bug reports, game setups, ideas and code are all welcome. Issues and discussions can be written in English or Turkish.

## Ways to help

| You want to… | Go to |
|--------------|-------|
| Report a bug | [New issue → Bug report](https://github.com/MouseDrive/MouseDrive/issues/new/choose) |
| Ask a question or get setup help | [Discussions → Q&A](https://github.com/MouseDrive/MouseDrive/discussions/categories/q-a) |
| Suggest a feature | [Discussions → Ideas](https://github.com/MouseDrive/MouseDrive/discussions/categories/ideas) |
| Share settings for a game or car | [Discussions](https://github.com/MouseDrive/MouseDrive/discussions) |
| Report a security issue | [SECURITY.md](SECURITY.md) — never in a public issue |
| Change code or docs | A pull request (see below) |

For anything larger than a small fix, please start a discussion or comment on the issue first, so we can agree on the approach before you spend time on it.

## How this repository works

The public repository holds the source code every release is built from. Development happens on the maintainer's private branch, which also holds the test suite and developer tools; each release is exported from it with most code comments removed.

What this means for you:

- Pull requests are reviewed and merged here as usual. The maintainer then carries the change over to the development branch, with you as the author, so later exports keep it.
- The internal tests are not public. Please describe in your pull request how you tested the change (game, vJoy version, steps).
- Please do not edit `CHANGELOG.md`; the maintainer writes the entries when preparing a release.

## Building

Requirements: Windows 10/11, the stable [Rust](https://rustup.rs/) toolchain (MSVC) and, to run it, the [vJoy driver](https://github.com/BrunnerInnovation/vJoy).

```powershell
cargo build --release --manifest-path MouseDrive/Cargo.toml
# without the auto-updater (no network code)
cargo build --release --manifest-path MouseDrive/Cargo.toml --no-default-features
```

Before opening a pull request, run the checks CI runs:

```powershell
cargo fmt --manifest-path MouseDrive/Cargo.toml --check
cargo clippy --manifest-path MouseDrive/Cargo.toml --all-targets --all-features -- -D warnings
cargo clippy --manifest-path MouseDrive/Cargo.toml --all-targets --no-default-features -- -D warnings
```

The README's *Project layout* section explains what lives where.

## Code guidelines

Source paths below are relative to `MouseDrive/src/` in the [MouseDrive repository](https://github.com/MouseDrive/MouseDrive).

- Format with `rustfmt`; clippy must pass with `-D warnings` in both feature sets.
- No `unwrap()` / `expect()` outside tests. Handle the error and tell the user what happened and what to do; MouseDrive has no silent fallbacks.
- Every `unsafe` block needs a `// SAFETY:` comment that states why it is sound.
- The driving logic (`logic.rs`, `logic/`) stays pure: no Windows API calls and no clock reads; time comes in through the tick input.
- The control loop (`control/`) runs at 250 Hz: no blocking calls, file I/O or logging per tick.
- Every user-visible string goes into both `lang/en.rs` and `lang/tr.rs`.
- Keep dependencies few; discuss a new one before adding it. Network code belongs only to the `updater` feature.
- One logical change per pull request; keep refactors separate from behaviour changes.

## Commits and sign-off

- Short, imperative subjects with a type prefix: `feat:`, `fix:`, `docs:`, `refactor:`, `perf:`, `build:`, `ci:`, `chore:`.
- Sign off every commit (`git commit -s`). The `Signed-off-by: Your Name <email>` line certifies that you wrote the change or have the right to submit it, as described in the [Developer Certificate of Origin 1.1](https://developercertificate.org/).

## License

MouseDrive is licensed under [GPL-3.0-or-later](https://github.com/MouseDrive/MouseDrive/blob/main/LICENSE). Contributions are accepted under the same license, and you keep the copyright of your work. The license grants no rights to the MouseDrive name or logo.

## Code of conduct

Everyone taking part is expected to follow the [Code of Conduct](CODE_OF_CONDUCT.md).
