# 📦 Integrated Libraries

This folder contains **Altium Integrated Libraries** (`.IntLib`) — compiled libraries that bundle schematic symbols, footprints, and 3D models into a single file.

---

## 📂 Structure

Each category has its own folder:

```
Int_Library/<Category>/
├── <Category>.LibPkg                    ← Altium project (source of truth)
└── Project Outputs for <Category>/
    └── <Category>.IntLib                ← Compiled library (auto-generated)
```

The `.LibPkg` is the **editable source** — it references `.SchLib` and `.PcbLib` files from the main folders. The `.IntLib` is the **compiled output** that Altium uses at design time.

## 📋 Available categories

| Category | Contents |
|----------|----------|
| `74xx` | 74-series logic |
| `Audio` | Audio amplifiers, codecs |
| `Comparator` | Voltage comparators |
| `Connectors` | All connector types |
| `Isolator` | Optocouplers, digital isolators |
| `MCU` | Microcontrollers |
| `Memory` | Flash, RAM, EEPROM |
| `Motor_Driver` | Motor controllers and drivers |
| `Passive` | Resistors, capacitors, inductors |
| `Protection` | TVS, ESD, fuses |
| `Regulator_DC_DC` | Switching regulators, LDOs |
| `RF` | RF amplifiers, transceivers |
| `Switch` | Mechanical switches, relays |
| `Transcivers` | Bus transceivers (RS485, CAN, etc.) |

## 🛠️ How to use

1. Open Altium Designer.
2. `File → Open` → select the `.IntLib` from the `Project Outputs for <Category>/` folder.
3. Drag components from the **Libraries panel** into your schematic or PCB.
4. The symbol, footprint, and 3D model are all included — no extra linking needed.

## ➕ Adding a component to an IntLib

1. Open the `.LibPkg` in Altium.
2. Ensure the relevant `.SchLib` and `.PcbLib` are added as source files.
3. Add/edit your component in those source files.
4. **Recompile:** `Project → Compile Integrated Library`.
5. The `.IntLib` is regenerated automatically.

⚠️ **Always commit both** the `.LibPkg` (source) and the updated `.IntLib` (output).

**Full step-by-step →** [Adding a Component](../docs/ADDING_COMPONENT.md)

## ⚠️ Lock before you edit

`.LibPkg` and `.IntLib` files are binary. Lock before editing:
```bash
git lfs lock Int_Library/<Category>/<Category>.LibPkg
```
After pushing: `git lfs unlock Int_Library/<Category>/<Category>.LibPkg`

## 🔗 Related
- [Schematic Symbols](../Schematic_Symbols/) — source `.SchLib` files
- [Footprints](../Footprints/) — source `.PcbLib` files
- [Library Conventions](../docs/LIBRARY_CONVENTIONS.md) — naming and organization rules
