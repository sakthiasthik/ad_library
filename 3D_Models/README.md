# 🧊 3D Models

This folder contains **7,000+ 3D component models** in `.STEP` and `.STL` format, organized by component type.

---

## 📂 Structure

Models are grouped by category in `.<fmt>shapes` subdirectories:

```
3D_Models/
├── Capacitor_SMD.3dshapes/       ← SMD capacitors
├── Capacitor_THT.3dshapes/       ← Through-hole capacitors
├── Connector_JST.3dshapes/       ← JST connectors
├── Connector_Molex.3dshapes/     ← Molex connectors
├── Package_SO.3dshapes/          ← SOIC / SOP packages
├── Package_QFP.3dshapes/         ← QFP packages
├── Resistor_SMD.3dshapes/        ← SMD resistors
└── ... (100+ categories)
```

## 🛠️ How to use

### Linking to a footprint
1. In Altium, open the `.PcbLib` footprint.
2. `Place → 3D Body → Generic STEP Model`.
3. Browse to the model file in this folder.
4. Align to pads. Save.

**Use relative paths** — they work on any machine:
```
..\3D_Models\Capacitor_SMD.3dshapes\C_0805.STEP
```

### Adding a new model
Place it in the most specific matching category. If no folder matches exactly, create one following the naming convention: `<Category>_<SubType>.<fmt>shapes` (e.g., `Connector_Hirose.3dshapes`).

**Full process →** [Adding a Component](../docs/ADDING_COMPONENT.md)

## 📋 Incomplete models
See [TODO.md](TODO.md) for a list of models still needed. Contributions welcome!

## 📄 Credits
Many models are sourced from the KiCad 3D model library. Individual credits are in `CREDITS.md` files within each category folder.
