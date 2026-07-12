# 👣 Footprints

This folder contains **Altium PCB footprint libraries** (`.PcbLib`) converted from **KiCad 9.0** and tuned for Altium Designer. These define pad layouts, courtyards, and silkscreen for PCB layout.

---

## 📂 Contents
- 150+ `.PcbLib` files organized by component category and manufacturer.
- Footprints are **pre-linked** to 3D models in [`../3D_Models/`](../3D_Models/) where available.

## 🛠️ How to use
1. Open Altium Designer.
2. `File → Open` → select the `.PcbLib` file you need.
3. Place footprints from the **Libraries panel** into your PCB layout.

## 🧊 3D model linking
Footprints reference their 3D models via **relative paths** — works on any machine:
```
..\3D_Models\Capacitor_SMD.3dshapes\C_0805.STEP
```
If a model is missing, check [`3D_Models/TODO.md`](../3D_Models/TODO.md) — it may not exist yet.

## ⚠️ Before you edit
`.PcbLib` files are binary — Git can't merge them. **Pull first, tell the team which file you're editing, and push as soon as you're done** so two people don't edit the same file at once.

**Full process →** [Adding a Component](../docs/ADDING_COMPONENT.md)

## 📏 Layer assignments
Footprints in this library use standard KiCad→Altium layer mapping. See [Layer Stack Details](../Layer_Stack_Details.md) for the complete reference table (courtyard = M6/M7, assembly = M4/M5, 3D body = M10/M11, etc.).

## 📏 Naming rules
See [Library Conventions](../docs/LIBRARY_CONVENTIONS.md) for footprint naming standards.
