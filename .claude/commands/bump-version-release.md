---
name: bump-version-release
description: Workflow command scaffold for bump-version-release in orca.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /bump-version-release

Use this workflow when working on **bump-version-release** in `orca`.

## Goal

Bump the application version for a new release, updating version numbers and lockfiles for both JavaScript and Rust (Tauri) parts of the project.

## Common Files

- `package.json`
- `src-tauri/Cargo.toml`
- `src-tauri/Cargo.lock`
- `src-tauri/tauri.conf.json`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update version in package.json
- Update version in src-tauri/Cargo.toml
- Update src-tauri/Cargo.lock
- Update src-tauri/tauri.conf.json

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.