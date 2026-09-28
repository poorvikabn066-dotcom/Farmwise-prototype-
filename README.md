# Compact Solar-Powered Agarbatti Drying & Packaging System

## 1. System Flow

### 1.1 Drying → Packaging Pipeline

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

### 1.2 Power Flow

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



---

## 2. Solar Power System

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


### 2.1 packaging system Components  

| # | Component | Function |
|---|---|---|
| 1 | Arduino UNO R3 | Main controller |
| 2 | NEMA 17 stepper motor + A4988 driver | Rotates the grooved picking drum |
| 3 | DC geared motor (12V, 30–60 RPM) | Drives the conveyor belt |
| 4 | SG90 servo motors (×2) | One for the bag dropper gate, one for the folding flap |
| 5 | IR sensor module | Accurately counts stock (for clear film wrap / blister pack lines) |
| 6 | L298N motor driver or relay module | Controls the 12V DC conveyor motor |

---



