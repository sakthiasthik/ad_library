# 📚 Altium Library Collection

**Ready-to-use Altium Designer libraries** — schematic symbols, PCB footprints, 3D models, and compiled integrated libraries. Converted from KiCad 9.0, tuned for Altium, and continuously updated by the team.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Branches synced automatically](https://img.shields.io/badge/branches-auto--synced-green.svg)](docs/GIT_WORKFLOW.md)
[![PR-on-conflict safety net](https://img.shields.io/badge/conflicts-PR--protected-orange.svg)](docs/GIT_WORKFLOW.md#handling-binary-conflicts)

---

## What's inside

| Directory | Contents | Format |
|-----------|----------|--------|
| [`Schematic_Symbols/`](Schematic_Symbols/) | 230+ schematic symbol libraries | `.SchLib` |
| [`Footprints/`](Footprints/) | 150+ PCB footprint libraries | `.PcbLib` |
| [`3D_Models/`](3D_Models/) | 7,000+ 3D component models | `.STEP`, `.STL` |
| [`Int_Library/`](Int_Library/) | Compiled integrated libraries (symbol + footprint + 3D) | `.IntLib` |
| [`Images_asset/`](Images_asset/) | Reference screenshots & layer config images | `.PNG` |
| [`Script/`](Script/) | Altium automation scripts | `.PrjScr`, `.pas` |

**💡 Tip:** If you only need to pluck out a few components, browse `Schematic_Symbols/` and `Footprints/` and import them directly into Altium. If you want the full integrated experience, use the `.IntLib` files from `Int_Library/`.

---

## I want to…

| Task | Go here |
|------|---------|
| **Set up for the first time** | → [New Developer Guide](docs/NEW_DEVELOPER.md) |
| **Add a new component** | → [Adding a Component](docs/ADDING_COMPONENT.md) |
| **Understand Git & branches** | → [Git Workflow](docs/GIT_WORKFLOW.md) |
| **See naming rules & structure** | → [Library Conventions](docs/LIBRARY_CONVENTIONS.md) |
| **Keep a checklist while I work** | → [Component Checklist](NEW_COMPONENT_CHECKLIST.md) |
| **Request a new component / report a bug** | → [Open an Issue](https://github.com/sakthiasthik/ad_library/issues/new/choose) |
| **See KiCad → Altium layer mapping** | → [Layer Stack Details](Layer_Stack_Details.md) |

---

## 🔑 The one rule for binary files

Altium files (`.SchLib`, `.PcbLib`, `.IntLib`) are **binary** — Git can't merge them. So there's just one rule:

> **Don't let two people edit the *same* file at the same time.**

How to stay safe (no locking, no read-only files):
1. **Pull before you start** — `git checkout dev && git pull`
2. **Tell the team** which library file you're about to edit (a quick message is enough).
3. **Push as soon as you're done** — don't sit on changes for days.

If an overlap ever happens, the auto-sync bot **opens a Pull Request instead of overwriting** — nobody loses work. **[Full guide →](docs/GIT_WORKFLOW.md)**

---

## 🔄 Branches auto-sync

Push to your `dev-<name>` branch → a bot merges it into `dev` → fans `dev` out to everyone else. **Never pushes to `main` or `dev` directly.** No config needed — any branch named `dev-*` is picked up automatically.

**[How it works →](docs/GIT_WORKFLOW.md#the-auto-sync-flow-what-happens-when-you-push)**

---

## 🗺️ Repo map

```
ad_library/
├── Schematic_Symbols/       ← .SchLib files (one per category)
├── Footprints/              ← .PcbLib files (one per category)
├── 3D_Models/               ← .STEP/.STL files (7k+ models)
├── Int_Library/             ← Compiled .IntLib (category.LibPkg + Project Outputs/)
├── Images_asset/            ← Screenshots & config references
├── Script/                  ← Altium automation
├── docs/                    ← (You are reading these) — process guides
│   ├── NEW_DEVELOPER.md
│   ├── ADDING_COMPONENT.md
│   ├── GIT_WORKFLOW.md
│   └── LIBRARY_CONVENTIONS.md
├── NEW_COMPONENT_CHECKLIST.md
├── Layer_Stack_Details.md
├── .github/
│   ├── workflows/sync.yml   ← Auto-sync action
│   ├── ISSUE_TEMPLATE/      ← Bug & feature request forms
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── CODEOWNERS
└── LICENSE                  ← MIT
```

---

## 📅 Ongoing work

- [ ] PCB Layer Stack Management — standard footprint layer assignments, via importer scripts and templates ([reference](Layer_Stack_Details.md))
- [ ] More 3D models for connectors, packages, and passives ([TODO list](3D_Models/TODO.md))
- [ ] Altium scripting support for batch operations

---

## 📜 License

MIT — see [LICENSE](LICENSE).

## 💬 Questions?

[Open an issue](https://github.com/sakthiasthik/ad_library/issues/new/choose) or start a discussion. Contributions welcome — just follow the [new developer guide](docs/NEW_DEVELOPER.md).
