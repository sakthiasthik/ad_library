# 📐 Schematic Symbols

This folder contains **Altium schematic symbols** (`.SchLib`) converted from **KiCad 9.0** libraries and tuned for Altium Designer.

---

## 📂 Contents
- 230+ `.SchLib` files covering analog, amplifiers, connectors, MCUs, regulators, passives, logic, RF, and more.
- Each file contains multiple symbols grouped by category.

## 🛠️ How to use
1. Open Altium Designer.
2. `File → Open` → select the `.SchLib` file you need.
3. Import symbols from the **Libraries panel** into your schematic.

## ⚠️ Lock before you edit
These files are **binary** — Git can't merge them. Before editing any `.SchLib`:
```bash
git lfs lock Schematic_Symbols/<file>.SchLib
```
After pushing: `git lfs unlock Schematic_Symbols/<file>.SchLib`

**Full process →** [Adding a Component](../docs/ADDING_COMPONENT.md)

## 📏 Naming rules
See [Library Conventions](../docs/LIBRARY_CONVENTIONS.md) for symbol naming standards (`Manufacturer_MPN_Description`).

## 🖼️ Reference
- [Layer Stack Details](../Layer_Stack_Details.md) — KiCad → Altium layer mapping
- [Root README](../README.md) — overview and branch workflow
