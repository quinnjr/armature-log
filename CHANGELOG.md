# Changelog — `armature-log`

All notable changes to this crate will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this crate adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Earlier changes are recorded in the workspace [`CHANGELOG.md`](../CHANGELOG.md).

## [Unreleased]

## [0.2.3] - 2026-09-15

### Changed

- Bumped resolved versions of `log`, `once_cell`, `chrono`, `tracing`, `tracing-subscriber`, `colored`, `serde`, `serde_json`, and the dev-dependency `tokio` to their latest compatible releases as part of a workspace-wide dependency upgrade. Manifest requirements were already loose enough (`"0.4"`, `"3.1"`, `"1"`, etc.) that no `Cargo.toml` version bump was needed, and no source changes were required — the crate builds, clippy is clean, and all 34 tests plus 8 doctests pass unchanged against the upgraded dependency graph.

## [0.2.2] - 2026-08-04

### Fixed

- Requirements on sibling armature crates name a minor instead of `0`. Under
  Cargo's 0.x rules `version = "0"` matches any release ever made, and edition
  2024 selects the MSRV-aware resolver, so a consumer declaring an older
  `rust-version` was handed the oldest version satisfying it — resolving
  `armature-core = "0"` on Rust 1.89 produced `armature-core 0.2.3` while an
  explicit `armature-core = "0.8"` elsewhere in the same graph pulled 0.8.2.
  Two copies of core, and a build failing on symbols the older one lacks. Each
  0.x minor in this family is a breaking change, so the requirement now names
  one. No API change.
