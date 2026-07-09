# 👋 New Developer Setup

Welcome to the **Altium Library Collection** — a shared library of schematic symbols, footprints, 3D models, and integrated libraries for Altium Designer.

This guide gets you from zero to making your first contribution in about 5 minutes.

---

## 1. Prerequisites

| Tool | Version | Check with |
|------|---------|------------|
| **Altium Designer** | 21+ | — |
| **Git** | 2.30+ | `git --version` |
| **Git LFS** | 3.0+ | `git lfs version` |

### Install Git LFS (one-time per computer)

```bash
git lfs install
```

If `git lfs` is not found, download it from [git-lfs.com](https://git-lfs.com).

---

## 2. Clone the repository

```bash
git clone git@github.com:sakthiasthik/ad_library.git
cd ad_library
```

Git LFS will automatically download the large binary files (3D models, IntLibs) during clone.

---

## 3. Create your own branch

**Every developer works in their own `dev-*` branch.** Never push directly to `main` or `dev`.

```bash
git checkout dev             # always branch FROM dev
git checkout -b dev-YOURNAME  # e.g. dev-sakthi, dev-srigowd
git push -u origin dev-YOURNAME
```

Your branch is now tracked. The auto-sync workflow will pick it up with zero config.

---

## 4. Understand the golden rule

> **🔒 Lock → Edit → Push → Unlock**

Our library files (`.SchLib`, `.PcbLib`, `.IntLib`) are **binary**. Git cannot merge them. If two people edit the same file, one person's work is destroyed.

File locking prevents this entirely. **Before touching any library file in Altium, lock it:**

```bash
git lfs lock Schematic_Symbols/Regulator_Switching.SchLib
```

After pushing your change, unlock it:

```bash
git lfs unlock Schematic_Symbols/Regulator_Switching.SchLib
```

**See who holds what:** `git lfs locks`
**Admin override (stuck lock):** `git lfs unlock <file> --force`

---

## 5. Before your first change — read these

| Document | Why |
|----------|-----|
| [Adding a Component](ADDING_COMPONENT.md) | Step-by-step: symbol → footprint → 3D → IntLib → push |
| [Library Conventions](LIBRARY_CONVENTIONS.md) | Naming rules, folder structure, when to create new libraries |
| [Git Workflow](GIT_WORKFLOW.md) | Branch strategy, auto-sync, handling conflicts |
| [Component Checklist](../NEW_COMPONENT_CHECKLIST.md) | Keep this open while you work — tick off each step |

---

## 6. The auto-sync — what happens when you push

When you push changes to `dev-YOURNAME`:

1. GitHub Actions merges your branch into `dev`.
2. Then it fans `dev` out to every other `dev-*` branch.

If a merge **can't be done cleanly** (because someone else edited the same binary file), the bot opens a Pull Request instead of silently overwriting anything. [Learn more →](GIT_WORKFLOW.md)

Check it running: **GitHub → Actions tab → `sync-branches` workflow.**

---

## 7. Quick reference card

```bash
# Lock a file before editing
git lfs lock <path>

# See all current locks
git lfs locks

# Unlock after push
git lfs unlock <path>

# Start fresh (one-time)
git lfs install
```

---

## Need help?

- Open an [Issue](https://github.com/sakthiasthik/ad_library/issues) — use the template that matches your problem.
- Ask in your team channel.
