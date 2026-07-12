# ✅ New Component Checklist

> **📋 Copy this into your PR description** and check off each step as you go.

---

## Before you start

- [ ] I read the [Library Conventions](docs/LIBRARY_CONVENTIONS.md) and my component follows the naming rules
- [ ] I pulled the latest `dev` before starting: `git checkout dev && git pull`
- [ ] I told the team which library file(s) I'm editing (so two people don't edit the same file)

## Component

| Detail | Value |
|--------|-------|
| **Manufacturer** | |
| **MPN (part number)** | |
| **Description** | |
| **Category** | |
| **Datasheet link** | |
| **Component name in library** | `MFG_MPN_Description` |

## Schematic symbol

- [ ] Created in the correct `.SchLib` file: `________________`
- [ ] Pin names, pin numbers, and electrical types match the datasheet
- [ ] Designator and comment fields are set correctly
- [ ] Symbol saved — no unsaved changes in Altium

## Footprint

- [ ] Created in the correct `.PcbLib` file: `________________`
- [ ] Pad dimensions, pitch, and paste mask match the datasheet
- [ ] Courtyard boundary added (Mechanical M6/M7) with adequate clearance
- [ ] Silkscreen outline doesn't overlap pads
- [ ] Footprint name matches the reference in the symbol

## 3D Model

- [ ] 3D model (`.STEP` or `.STL`) placed in correct folder: `3D_Models/________________`
- [ ] Model linked in the footprint with **relative path**
- [ ] Model aligned to pads (no offset, correct orientation)
- [ ] *(or)* No 3D model available yet → noted in commit message

## Integrated Library

- [ ] Component added to the correct `.LibPkg`: `________________`
- [ ] LibPkg recompiled — `.IntLib` updated in `Project Outputs for <Category>/`
- [ ] No ERC errors after compilation

## Commit & push

- [ ] Committed with a clear message: `Add/Update <MPN> - <Description>`
- [ ] Pushed to my branch: `git push origin dev-________`
- [ ] Checked [GitHub Actions](https://github.com/sakthiasthik/ad_library/actions) — `sync-branches` workflow is green ✅
  - [ ] If a PR opened instead, I'm resolving the binary conflict ([guide](docs/GIT_WORKFLOW.md#handling-binary-conflicts))

## Cleanup

- [ ] Pushed promptly so the file isn't held edited-but-unshared for long
- [ ] Confirmed the `sync-branches` workflow is green (or resolved the PR if one opened)

---

## Files changed

| File | Change (new / modified / deleted) |
|------|-----------------------------------|
| | |
| | |
| | |

---

## Notes for the reviewer

<!-- Anything the reviewer should know? e.g. "used TI datasheet Rev C", "3D model from SnapEDA", "reused existing SOT-23-5 footprint" -->
