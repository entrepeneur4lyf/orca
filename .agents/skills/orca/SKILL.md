```markdown
# orca Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches the key development patterns, coding conventions, and workflows used in the `orca` repository—a TypeScript project using the Vite framework with a Tauri (Rust) backend. You'll learn how to structure code, manage dependencies, coordinate frontend and backend changes, and follow the repository's established workflows for releases, features, and bugfixes.

## Coding Conventions

- **File Naming:**  
  Use camelCase for file names.  
  _Example:_  
  ```
  src/components/userProfile.tsx
  src/pages/settingsPage.tsx
  ```

- **Import Style:**  
  Use alias-based imports for modules.  
  _Example:_  
  ```typescript
  import { Button } from '@/components/button'
  import { fetchData } from '@/utils/api'
  ```

- **Export Style:**  
  Mixed usage of named and default exports.  
  _Example:_  
  ```typescript
  // Named export
  export function doThing() { ... }

  // Default export
  export default MyComponent
  ```

- **Commit Patterns:**  
  - Freeform commit messages (no strict prefixes)
  - Average message length: ~38 characters

## Workflows

### bump-version-release
**Trigger:** When releasing a new version of the app  
**Command:** `/bump-version`

1. Update the version in `package.json`
2. Update the version in `src-tauri/Cargo.toml`
3. Update `src-tauri/Cargo.lock`
4. Update `src-tauri/tauri.conf.json`
5. Commit all changes with a message like:  
   ```
   Bump version to vX.Y.Z
   ```

_Example:_  
```bash
# Manually update version numbers in the files above
git add package.json src-tauri/Cargo.toml src-tauri/Cargo.lock src-tauri/tauri.conf.json
git commit -m "Bump version to v1.2.3"
```

---

### dependency-update-cargo-lock
**Trigger:** When upgrading a Rust crate dependency  
**Command:** `/update-cargo-dep`

1. Update the dependency version in `src-tauri/Cargo.toml` (or let Dependabot do this)
2. Regenerate `Cargo.lock` (typically via `cargo update`)
3. Commit the updated `Cargo.lock` file

_Example:_  
```bash
cd src-tauri
cargo update
git add Cargo.lock
git commit -m "Update Rust dependencies"
```

---

### feature-or-bugfix-ui-and-changelog
**Trigger:** When adding a new UI feature or fixing a UI bug and documenting it  
**Command:** `/feature-ui`

1. Edit one or more files in `src/components/*.tsx` or `src/pages/*.tsx`
2. Update `CHANGELOG.md` with a description of the change
3. Commit your changes

_Example:_  
```typescript
// src/components/newFeature.tsx
export function NewFeature() { ... }
```
```markdown
# CHANGELOG.md
- Added NewFeature component to improve UX
```
```bash
git add src/components/newFeature.tsx CHANGELOG.md
git commit -m "Add NewFeature component and update changelog"
```

---

### feature-or-bugfix-tauri-rust-and-ui
**Trigger:** When adding or fixing a feature that spans both the Tauri backend and the React frontend  
**Command:** `/feature-tauri-ui`

1. Edit backend logic in `src-tauri/src/*.rs`
2. Edit frontend logic in `src/components/*.tsx` or `src/pages/*.tsx`
3. Optionally update `CHANGELOG.md`
4. Commit all related changes

_Example:_  
```rust
// src-tauri/src/new_feature.rs
pub fn new_feature() { ... }
```
```typescript
// src/components/NewFeature.tsx
import { invoke } from '@tauri-apps/api/tauri'
export function NewFeature() {
  // Call Rust backend
  invoke('new_feature')
}
```
```bash
git add src-tauri/src/new_feature.rs src/components/NewFeature.tsx
git commit -m "Add new_feature to backend and UI"
```

## Testing Patterns

- **Test File Pattern:**  
  Test files follow the `*.test.*` naming convention.
  _Example:_  
  ```
  src/components/button.test.tsx
  src/utils/api.test.ts
  ```

- **Testing Framework:**  
  Not explicitly detected; check the repository for specifics (e.g., Jest, Vitest).

## Commands

| Command             | Purpose                                                        |
|---------------------|----------------------------------------------------------------|
| /bump-version       | Bump app version for a new release (JS & Rust parts)           |
| /update-cargo-dep   | Update Rust dependencies and regenerate Cargo.lock             |
| /feature-ui         | Add or fix a UI feature/bug and update the changelog           |
| /feature-tauri-ui   | Add or fix a feature spanning both Tauri backend and frontend  |
```