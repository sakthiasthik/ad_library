# 🔄 Git Workflow & Branch Strategy

This repo uses a **dev-branch fan-out** pattern with automatic sync. Here's how it works and how to handle every situation.

---

## Branch structure

```
main  ←── (manual merges, protected, never push directly)
  └─ dev  ←── (single source of truth, auto-synced from dev-* branches)
       ├─ dev-sakthi
       ├─ dev-srigowd
       └─ dev-YOURNAME  ← any branch named dev-*
```

- **`main`** — protected. Only manual merges from `dev` for releases.
- **`dev`** — the integration branch. Never edited directly. Updated by the bot.
- **`dev-YOURNAME`** — your personal working branch. Push here.

---

## The auto-sync flow (what happens when you push)

```
You push to dev-sakthi
  │
  ▼
  1. GitHub Action: merges dev-sakthi ──→ dev
     ├─ clean? ✅ pushed to dev
     └─ conflict? ⚠️ opens a Pull Request (NO overwriting)
            │
            ▼
  2. dev ──→ fast-forward to: dev-srigowd, dev-dhanush, dev-<anyone>
     ├─ clean FF? ✅ pushed
     └─ can't FF? ⚠️ opens a PR (branch has its own commits)
```

**Safety rule:** the automation NEVER force-overwrites. It either:
- merges/fast-forwards cleanly, OR
- opens a Pull Request for a human to handle.

---

## The daily workflow

```bash
# 1. Start from the latest dev
git checkout dev
git pull origin dev
git checkout -b dev-YOURNAME

# 2. (Coordinate) Tell the team which library file you're editing

# 3. Edit in Altium, save, commit
git add Schematic_Symbols/SomeFile.SchLib
git commit -m "Add XYZ component"

# 4. Push
git push origin dev-YOURNAME

# 5. Verify the bot synced (Actions tab → green ✅)
#    If a PR opened instead → see "Handling binary conflicts" below
```

---

## Handling binary conflicts

**Scenario:** You edited `Regulator_Switching.SchLib`. At the same time, Srigowd also edited it on `dev-srigowd`, and the bot already merged his change into `dev`. Now your merge into `dev` creates a **binary conflict** — Git can't line-by-line merge a `.SchLib`.

What happens:
1. The bot **does NOT silently overwrite** anyone's work.
2. It opens a Pull Request labeled *"Manual merge needed: dev-sakthi → dev"*.
3. **You must resolve this in Altium, not in git:**

### How to resolve

```bash
# Checkout dev and see what's on the branch
git checkout dev
git pull origin dev

# Create a resolution branch
git checkout -b merge/dev-sakthi-to-dev

# Merge your branch in (this will show the conflict)
git merge dev-sakthi
# Git reports: CONFLICT (content): Regulator_Switching.SchLib
```

**Now — open the conflicting `.SchLib` in Altium:**

1. Open **both versions** side-by-side.
2. Manually copy your new component into the library that has the other person's component already in it.
3. Save the combined `.SchLib`.
4. Mark the conflict as resolved in git:

```bash
git add Schematic_Symbols/Regulator_Switching.SchLib
git commit -m "resolve: merge dev-sakthi Regulator_Switching changes"
git push origin merge/dev-sakthi-to-dev
```

5. Merge that branch's PR. The bot then fans `dev` out to everyone.

---

## When `dev` moved ahead of your branch (syncing from upstream)

Srigowd pushed first, the bot updated `dev`, and now your `dev-sakthi` is behind:

```bash
git checkout dev-sakthi
git fetch origin
git merge origin/dev   # pull latest dev into your branch
# Binary conflict? Open both .SchLib side-by-side in Altium, combine manually.
git push origin dev-sakthi
```

---

## Avoiding clashes (instead of locking)

We deliberately do **not** use file locking or read-only files — they caused too much friction (especially on Windows, where `git lfs lock` is unreliable). Instead, avoid clashes with three simple habits:

1. **Pull before you start.** `git checkout dev && git pull` so you're editing the newest version.
2. **Announce the file.** A one-line message ("editing Regulator_Switching.SchLib") stops two people opening the same file.
3. **Push quickly.** The longer a file sits edited-but-unpushed, the more likely someone else touches it.

### What if two people edit the same file anyway?

You're still protected. The auto-sync bot **never overwrites** — it opens a Pull Request so a human combines both changes in Altium. See [Handling binary conflicts](#handling-binary-conflicts).

### Best long-term fix: split libraries by owner

Give each person their own library files (e.g. Sakthi owns `Regulator_*`, Srigowd owns `Connector_*`). Then clashes basically can't happen. See [Library Conventions](LIBRARY_CONVENTIONS.md).

---

## Recovering from a force-push

If a branch history gets rewritten (e.g., removing bad commits), everyone who had a local copy must:

```bash
git fetch origin
git checkout <branch-name>
git reset --hard origin/<branch-name>
```

This discards your local version of that branch and matches the remote exactly.

---

## Rollback / restore (backup tags)

Branches deleted during cleanup are saved as tags:

| Deleted branch | Backup tag |
|----------------|------------|
| `dev-dhanush` | `backup-dev-dhanush-20260709` |
| `dev-sachin` | `backup-dev-sachin-20260709` |
| `developement` | `backup-developement-20260709` |
| `sub_development_1` | `backup-sub_development_1-20260709` |

To restore: `git branch <name> <tag> && git push origin <name>`

---

## FAQ

**Q: Can I push directly to `main`?** No. It's protected. Use PRs from `dev`.

**Q: Can I push directly to `dev`?** Don't. The bot manages `dev`. Push to your `dev-*` branch and let the bot integrate.

**Q: I created a new `dev-*` branch. Will it auto-sync?** Yes — the workflow uses wildcard matching (`dev-*`) and dynamic branch discovery. Zero config needed.

**Q: The bot synced wrong — can I revert?** Yes. The bot creates merge commits that are normal git history. Use `git revert <merge-commit>` on `dev`, push manually (bot won't overwrite a non-FF), then notify the team.
