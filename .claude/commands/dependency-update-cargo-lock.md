---
name: dependency-update-cargo-lock
description: Workflow command scaffold for dependency-update-cargo-lock in orca.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /dependency-update-cargo-lock

Use this workflow when working on **dependency-update-cargo-lock** in `orca`.

## Goal

Update Rust dependencies in the Tauri backend, typically via Dependabot or manual cargo update, resulting in changes to Cargo.lock.

## Common Files

- `src-tauri/Cargo.lock`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update dependency version in Cargo.toml (sometimes implicit via PR)
- Regenerate Cargo.lock
- Merge or commit the updated lockfile

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.