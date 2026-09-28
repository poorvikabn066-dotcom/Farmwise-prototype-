# Compact Solar-Powered Agarbatti Drying & Packaging System

An automated, solar-powered system to dry agarbatti (incense sticks) and then count, bundle, and pack them — reducing manual labor in small-scale agarbatti production.

> **Status:** Concept / design stage — component list and system flow drafted, subsystems not yet built or tested. This README consolidates initial planning notes.

---

## 1. Overview

The system has two main stages:

1. **Drying Stage** — solar-heated chamber that dries wet-rolled agarbatti sticks.
2. **Packaging Stage** — automated counting, bundling, wrapping, and packing of dried sticks.

The whole system is designed to run off solar power (panel + charge controller + battery), making it suitable for off-grid or rural production units.

---

## 2. System Flow

### 2.1 Drying → Packaging Pipeline

```
Dried Agarbatti
      ↓
    Hopper
      ↓
 NEMA 17 Feeder
      ↓
 IR Sensor (counts sticks)
      ↓
 Required Quantity Reached?
      ↓
 Automatic Stopper / Bundling
      ↓
 Craft Paper Wrapping
      ↓
 Finished, Packed Agarbatti
```

### 2.2 Power Flow

```
Solar Panel
      ↓
Charge Controller
      ↓
    Battery
    ├── Drying subsystem
    └── Packaging subsystem
```

---

## 3. Drying Subsystem

| Aspect | Notes / Open Questions |
|---|---|
| Solar panel | ~100W size, efficiency TBD |
| Solar air collector | For heating intake air |
| Controller | ESP32 — handles programming & control logic |
| Drying plate/tray | Material, size, and stick capacity TBD |
| Environment sensing | Temperature, humidity, moisture — need to define target range |
| Weighing | Load cell for measuring dried stick batches (TBD) |
| Tilting mechanism | Servo motor — for tray tilting/unloading |
| Chamber | Design & material TBD |
| Ventilation | DC fan / exhaust fan — capacity, energy draw, size & speed TBD |
| System design | Needs a block diagram and full flowchart |
| Power budget | Total power/energy consumption not yet calculated |

**Load cell considerations:** movement during weighing, calibration, and vibration need to be accounted for in the design.

---

## 4. Solar Power System

```
Solar Panel → Charge Controller → Battery → (Drying + Packaging loads)
```

- **Charge controller function:** senses voltage & current, regulates charging current via MOSFET, inductor, diode, etc.
- **Example calculation:** if solar panel = 18V and battery = 12.7V, roughly 4A of current flows.
- **Power formula:** `P = V_panel × I_panel`

### Candidate Charge Controllers

| Model | Spec | Approx. Price |
|---|---|---|
| UTL 20A | 12/24V solar | ~₹1.7k |
| Sparkel | 12V 20A Li-MPPT | ~₹3.45k |

**Open item:** Battery type, capacity, and backup runtime still to be decided.

---

## 5. Packaging Subsystem

### 5.1 Packing Method Options

- **Primary packing:**
  - Shrink sleeving & flow wrapping
  - Blister packing
- **Budget range:** ₹2,000 – ₹3,500 (for packing mechanism/materials)
- Clear film wrap option under consideration
- "Smart-Belt" concept — conveyor with banner/light-curtain sensor + servo motor

### 5.2 Three Primary Steps

1. **Singulation** — separating individual sticks/bundles
2. **Counting** — accurate stick count via sensor
3. **Wrapping / Sealing** — final packaging

> **Known difficulty:** the singulation/picking drum mechanism is expected to be the hardest part to get right.

### 5.3 Components

| # | Component | Function |
|---|---|---|
| 1 | Arduino UNO R3 | Main controller |
| 2 | NEMA 17 stepper motor + A4988 driver | Rotates the grooved picking drum |
| 3 | DC geared motor (12V, 30–60 RPM) | Drives the conveyor belt |
| 4 | SG90 servo motors (×2) | One for the bag dropper gate, one for the folding flap |
| 5 | IR sensor module | Accurately counts stock (for clear film wrap / blister pack lines) |
| 6 | L298N motor driver or relay module | Controls the 12V DC conveyor motor |

---

## 6. Open Questions / To Do

- [ ] Finalize solar panel wattage and efficiency target
- [ ] Choose drying plate material, size, and stick capacity
- [ ] Define target temperature / humidity / moisture ranges for drying
- [ ] Select load cell and finalize weighing mechanism (address vibration/calibration issues)
- [ ] Design drying chamber (material + layout)
- [ ] Size DC/exhaust fan (capacity, speed, power draw)
- [ ] Calculate total system power/energy budget
- [ ] Choose battery type, capacity, and backup strategy
- [ ] Finalize charge controller (UTL vs Sparkel vs alternatives)
- [ ] Decide packaging method (shrink sleeve/flow wrap vs blister pack)
- [ ] Design and prototype the picking/singulation drum
- [ ] Draw full system block diagram and flowchart
- [ ] Write ESP32/Arduino control logic (feeder, counting, stopper, packing sequence)

---

## 7. Repository Structure (suggested)

```
/hardware        — wiring diagrams, BOM, datasheets
/firmware        — ESP32 (drying) and Arduino UNO (packaging) code
/docs            — block diagrams, flowcharts, calculations
README.md        — this file
```

---

*This README was compiled from handwritten project notes and will be updated as the design progresses.*
