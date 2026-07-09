# Branch sync & file locking

This repo holds **Altium binary libraries** (`.SchLib`, `.PcbLib`, `.IntLib`).
Git cannot merge binary files line-by-line — if two people edit the same file on
two branches, one person's work is lost on merge. Two things keep this safe:

## 1. Automatic branch sync (`.github/workflows/sync.yml`)

When you push to your `dev-*` branch, a GitHub Action:

1. merges your branch into `dev`, then
2. fast-forwards `dev` out to the other `dev-*` branches.

If a merge is **not clean**, it does **not** overwrite anything — it opens a Pull
Request so the conflict is resolved by a human in Altium.

## 2. Lock a file before you edit it (Git LFS locking)

Because binary files can't be merged, claim a file before editing so nobody else
can change it at the same time:

```bash
git lfs lock   Schematic_Symbols/Regulator_Switching.SchLib   # before editing
# ... edit in Altium, commit ...
git push
git lfs unlock Schematic_Symbols/Regulator_Switching.SchLib   # release it
git lfs locks                                                  # who holds what
```

One-time setup per machine: `git lfs install`.

## Golden rule

**Never two people on the same library file at once.** Lock it, edit it, push,
unlock it. This is the only way to avoid losing schematic/footprint work.
