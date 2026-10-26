# Changelog

All notable **infrastructure, workflow, and documentation** changes to this repository.

Component additions (schematic symbols, footprints, 3D models) are tracked in the
[commit history](https://github.com/sakthiasthik/ad_library/commits) and are **not** repeated here —
this file records changes to *how the repo works*, not to its parts.

Format based on [Keep a Changelog](https://keepachangelog.com/).

---

## 2026-07-12 — Simpler collaboration (file locking removed)

### Changed
- **Removed read-only file locking.** `.SchLib` / `.PcbLib` / `.IntLib` files are now normal
  writable files. The `lockable` attribute had made them read-only until locked, which caused
  constant *"read only file"* errors in Altium — worst on Windows, where `git lfs lock` is
  unreliable and these files aren't even LFS-backed. (`d3fe2b6`)
- **New collaboration model:** *pull → announce the file → push promptly*, replacing
  *lock → edit → push → unlock*. The auto-sync workflow's "open a PR instead of overwriting"
  behavior remains the safety net against lost work.

### Removed
- The three `lockable` lines from `.gitattributes` (Git LFS storage for `.IntLib` kept).

### Documentation
- Updated `README.md`, all four `docs/` guides, the four folder READMEs,
  `NEW_COMPONENT_CHECKLIST.md`, and the PR template to the no-lock workflow.

---

## 2026-07-09 — Branch automation & documentation overhaul

### Added
- **Auto-sync workflow** — `.github/workflows/sync.yml`. On push to any `dev-*` branch it merges
  into `dev`, then fans `dev` out to every other `dev-*` branch. On a binary conflict it opens a
  **Pull Request instead of overwriting**. Uses a `dev-*` wildcard trigger with dynamic branch
  discovery, so **new `dev-*` branches are covered automatically** — no config edits needed.
  (`8ac45c8`, upgraded in `b4fa68f`)
- **Onboarding & process guides** under `docs/`:
  - `NEW_DEVELOPER.md` — first-day setup (clone, branch, workflow)
  - `ADDING_COMPONENT.md` — step-by-step guide to add a part
  - `GIT_WORKFLOW.md` — branch strategy, auto-sync, binary conflict resolution
  - `LIBRARY_CONVENTIONS.md` — naming rules, folder structure, IntLib categories
- **Templates & helper files:**
  - `NEW_COMPONENT_CHECKLIST.md` — copy-paste checklist per component
  - `.github/PULL_REQUEST_TEMPLATE.md` — auto-fills every PR with a checklist
  - `.github/ISSUE_TEMPLATE/new-component.yml` — structured component request form
  - `.github/ISSUE_TEMPLATE/bug.yml` — structured library problem report form
  - `.github/CODEOWNERS` — reviewer routing (template)
- *(Initial, removed 2026-07-12)* Git LFS file locking via `lockable` in `.gitattributes`.

### Changed
- **Rewrote `README.md`** as a documentation hub — short intro, badges, visual folder map, and an
  "I want to…" link tree to every guide. Tutorial content moved into `docs/`. (`c9bef2a`)
- **Refreshed the four folder READMEs** (`Schematic_Symbols/`, `Footprints/`, `Int_Library/`,
  `3D_Models/`) with links back to the process guides.
- Added a header and hub link to `Layer_Stack_Details.md`.

### Removed
- **Deleted stale branches** (each preserved as a `backup-*-20260709` tag):
  `dev-dhanush`, `dev-sachin`, `developement`, `sub_development_1`.
  The repository now has four branches: `main`, `dev`, `dev-sakthi`, `dev-srigowd`.
- `BRANCH_SYNC.md` — content folded into `docs/GIT_WORKFLOW.md`.

### Fixed
- **Resolved the `dev-sakthi` ↔ `dev-srigowd` merge conflict.** Removed the last two commits from
  `dev-srigowd` (TPS61023DRLR work, `e6020b1` + `bd32850`; preserved in tag
  `backup-dev-srigowd-20260709`), merged `dev-sakthi` into `dev`, and realigned `dev-srigowd`.
  All three branches converged cleanly.

---

## Recovery reference

Nothing was permanently deleted — every removed branch and commit is preserved as a tag:

| Backup tag | Restores |
|------------|----------|
| `backup-dev-srigowd-20260709` | The 2 removed TPS61023DRLR commits |
| `backup-dev-dhanush-20260709` | `dev-dhanush` branch |
| `backup-dev-sachin-20260709` | `dev-sachin` branch |
| `backup-developement-20260709` | `developement` branch |
| `backup-sub_development_1-20260709` | `sub_development_1` branch |

**Restore a branch:** `git branch <name> <tag> && git push origin <name>`
**Restore the TPS commits:** `git cherry-pick e6020b1 bd32850`
