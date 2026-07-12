# ➕ Adding a New Component

Follow these steps every time you add or modify a component in the library. **Keep the [Checklist](../NEW_COMPONENT_CHECKLIST.md) open** and tick off each step as you go.

---

## Overview

```
✏️ Symbol  →  🦶 Footprint  →  🧊 3D Model  →  📦 IntLib  →  📝 Commit  →  🚀 Push
```

> **Before you start:** pull the latest `dev`, and tell the team which library file you'll edit so two people don't touch the same file at once.

---

## Step 0: Start from the latest code

**Before opening Altium**, make sure you have the newest version and won't clash with anyone.

```bash
git checkout dev
git pull origin dev
git checkout -b dev-YOURNAME   # or switch to your existing branch
```

Then send a quick message to the team: *"editing Regulator_Switching.SchLib"*. That one line is all it takes to avoid two people editing the same binary file.

---

## Step 1: Create or edit the schematic symbol

1. Open Altium Designer.
2. `File → Open` the relevant `.SchLib` file from `Schematic_Symbols/`.
3. Create the new symbol or edit an existing one.
4. **Naming convention:** `Manufacturer_MPN_Description`
   - Example: `TI_TPS61023DRLR_Boost_Converter`
5. Assign a footprint reference (you'll create it in Step 2).
6. Save the `.SchLib` file and close.

**Never two symbols with the same name in one `.SchLib`** — Altium will silently overwrite one.

---

## Step 2: Create or edit the footprint

1. In Altium, `File → Open` the relevant `.PcbLib` file from `Footprints/`.
2. Create the footprint with exact pad dimensions, courtyard, and silkscreen from the datasheet.
3. **Naming convention:** match the footprint reference from Step 1.
4. Save the `.PcbLib` file.

📐 **Layer mapping reference:** See [Layer Stack Details](../Layer_Stack_Details.md) for the KiCad→Altium mechanical layer mapping used in this library.

---

## Step 3: Import and link the 3D model

1. Get the `.STEP` or `.STL` file for your component (from manufacturer, SnapEDA, or generate it).
2. Place it in the correct category folder under `3D_Models/`.
   - Path: `3D_Models/<Category>.<subcategory>/<model>.STEP`
3. In the footprint editor, go to `Place → 3D Body → Generic STEP Model`.
4. Browse to the 3D model file and embed it (use **relative path**).
5. Align the model to the footprint pads.
6. Save the `.PcbLib`.

---

## Step 4: Build/recompile the Integrated Library (.IntLib)

### Option A: Existing IntLib (add component to existing `.LibPkg`)

1. `File → Open` the `.LibPkg` file from `Int_Library/<Category>/`.
2. If not already present, add your `.SchLib` as a source.
3. In the LibPkg, right-click the `.SchLib` and select **Compile**.
4. `Project → Compile Integrated Library`.
5. The updated `.IntLib` appears in `Project Outputs for <Category>/`.

### Option B: New IntLib category (create a new folder)

1. Create `Int_Library/<NewCategory>/`.
2. In Altium: `File → New → Project → Integrated Library`.
3. Save the `.LibPkg` in the new folder.
4. Add your `.SchLib` and `.PcbLib` as sources.
5. Compile → the `.IntLib` is generated in `Project Outputs for <NewCategory>/`.

📂 **Full structure reference:** [Library Conventions](LIBRARY_CONVENTIONS.md)

---

## Step 5: Commit your changes

```bash
git add Schematic_Symbols/Regulator_Switching.SchLib
git add Footprints/TI.PcbLib
git add Int_Library/Regulator_DC_DC/
git add 3D_Models/<new-model>.STEP
git commit -m "Add TPS61023DRLR boost converter"
```

💡 **Commit message tip:** Use `Manufacturer PartNumber - Category` format. Keep it short and searchable.

---

## Step 6: Push your branch

```bash
git push origin dev-YOURNAME
```

The auto-sync bot merges your branch into `dev`, then fans `dev` out to all other `dev-*` branches. [Learn how →](GIT_WORKFLOW.md)

**Go to the Actions tab** and confirm the `sync-branches` workflow completed green ✅. This is important — if it opened a PR instead, you have a binary conflict that needs manual resolution.

---

## Step 7: Confirm it synced

Go to the **Actions tab** and confirm the `sync-branches` workflow finished green ✅.

- ✅ Green → your component is now in `dev` and synced to the whole team.
- ⚠️ A PR opened instead → you have a binary conflict (someone edited the same file). See [Resolving Conflicts](GIT_WORKFLOW.md#handling-binary-conflicts).

---

## Done! ✅

Your component is now in `dev` and synced to the whole team.

If the auto-sync opened a PR (binary conflict), see [Resolving Conflicts](GIT_WORKFLOW.md#handling-binary-conflicts) in the Git Workflow guide.
