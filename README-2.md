# Solar-Powered Agarbatti Drying & Packaging Machine

**Problem Statement PS SIH26022** — Smart solar-powered drying and compact packaging system to support home-based agarbatti manufacturing by rural women artisans.

## 1. Problem

Home-based agarbatti (incense stick) makers currently dry freshly rolled sticks in open sunlight or ambient heat. This has several drawbacks:

- Open-sun drying typically takes 1–2 days per batch (longer in weak sun or humid weather) and depends entirely on the weather.
- Drying is difficult or impossible at night and on rainy/overcast days.
- Temperature and humidity are not monitored, so output quality is inconsistent.
- Packing (weighing, counting, sealing) is done fully by hand, which is slow and limits daily output.
- There is no low-cost, rural-friendly machine that combines drying and packaging in one unit.

## 2. Proposed Solution

A compact, wheeled machine that combines stick drying and packaging in a single unit, powered by a hybrid solar + 230 V grid supply so it can run in sunlight, at night, and in bad weather.

**Production flow:**

```
Forming & Coating → Drying (mesh-tray chamber) → Fragrance application →
Weighing/Counting → Heat Sealing → Packet Output
```

**Core idea:**

- Sticks are loaded onto removable stainless-steel mesh trays inside an enclosed drying chamber.
- A thermostat-controlled heater and fans dry the sticks in 4–5 hours instead of the 1–2 days open-sun drying can take.
- Once dry, each tray tilts automatically and slides the sticks onto a chute feeding the packaging section — removing manual unloading.
- An ESP32 microcontroller reads temperature/humidity/PIR sensors and automatically switches the heater, fans and fragrance pump.
- Power comes from a 100 Wp solar panel with battery backup, switching automatically to the 230 V grid when solar is insufficient.

## 3. Technical Approach

### 3.1 Drying Chamber — Mesh Tray & Tilting Design

The drying chamber holds 4 removable stainless-steel mesh trays stacked in a rack, each independently reachable by the hot-air stream from the heater and circulation fans.

| Parameter | Specification (indicative design values) |
|---|---|
| Tray size | 600 mm (L) × 400 mm (W) × 50 mm (deep) |
| Mesh opening | 3 mm × 3 mm woven stainless-steel mesh — holds stick base upright while allowing hot air through |
| Trays per unit | 4 trays, stacked with ~60 mm gap between them for airflow |
| Sticks per tray | ≈ 1,000 sticks, arranged upright in slotted mesh rows |
| Sticks per drying cycle | ≈ 4,000 sticks (4 trays) = one 2 kg batch, matching 40 packets of 50 g (100 sticks each) |
| Tilting mechanism | Small geared motor/servo tilts each tray to ~40–45° after the drying cycle ends |
| Unloading | Tilted tray slides dried sticks down a chute directly onto the weighing/packaging conveyor |
| Drying time per cycle | 4–5 hours (vs 1–2 days in open sun drying, weather-dependent) |

This tray-and-tilt design is what lets the same unit handle both drying and the hand-off into packaging, without a person manually lifting or emptying trays.

### 3.2 Solar Panel

| Parameter | Specification (typical 100 Wp panel) |
|---|---|
| Rated power | 100 Wp (polycrystalline/monocrystalline) |
| Panel size | ≈ 1000 mm (L) × 670 mm (W) × 30 mm (D) |
| Weight | ≈ 7.5–8 kg |
| Mounting | Fixed tilt frame, ~20–30° facing south, on top of or beside the machine cabinet |
| Output | Charge controller (40 A) → battery (12 V, 75 Ah) + heater controller |

### 3.3 Hybrid Power Arrangement

- Solar panel (100 Wp) → Charge controller (40 A) → 24 V heater controller → 500 W heater
- Solar panel → Charge controller → Battery (12 V, 75 Ah) → ESP32 / sensors / fans
- 230 V grid → 24 V AC-DC supply (600 W) → 24 V heater (backup)
- Solar runs the heater during useful sunlight; battery supports the controller, sensors, display and low-power loads; grid takes over when solar is insufficient or at night.
- A changeover switch + MCB handle source selection and protection.

### 3.4 Smart Control (ESP32)

```
Sensors (Temperature · Humidity · PIR) → ESP32 → Relays (heater, fans, pump) + Display + Buzzer/LEDs
```

The ESP32 continuously reads chamber temperature and humidity and switches the heater/fan relays to hold the target drying range.

### 3.5 Packaging System

Dried sticks slide off the tilted tray onto a short feed chute that leads into the packaging section, where bundling, weighing/counting and sealing happen in sequence.

| Parameter | Specification (indicative design values) |
|---|---|
| Feed | Chute from drying tray → bundling guide → weighing/counting station |
| Counting/weighing | IR break-beam stick counter or 0–100 g load cell (0.1 g resolution), preset to 100 sticks / 50 g per packet |
| Pouch | Pre-formed LDPE/BOPP poly pouch, ≈ 230 mm (L) × 70 mm (W) — sized for standard 9-inch (≈230 mm) agarbatti sticks bundled together |
| Sealing method | Impulse heat sealer, 100 W, ~150–180°C sealing temperature, 2–3 s seal time per packet |
| Packaging cycle | ≈ 40–45 s per packet (bundle → weigh → feed → seal) → up to ~80 packets/hour capacity |
| Output per batch | 40 packets per 4,000-stick (2 kg) drying batch |
| Output per day | ≈ 71 packets across an 8-hour working day (2 batches) |
| Collection | Sealed packets drop onto a small output tray/bin for manual pickup |

This keeps packaging semi-automatic: the machine handles counting, weighing and sealing; a person only needs to load raw sticks at the start and collect finished packets at the end.

## 4. Components List & Why Used

| # | Component | Rating | Why it's used |
|---|---|---|---|
| 1 | Heating element | 500 W | Dries sticks faster; thermostat holds target temperature |
| 2 | DC circulation/exhaust fans | 80 W | Air circulation and moisture removal from the chamber |
| 3 | Agarbatti forming motor | 150 W | Forms and coats the raw sticks |
| 4 | Fragrance pump | 20 W | Controlled, even fragrance application |
| 5 | Packaging / sealing unit | 100 W | Weighing and heat-sealing the packets |
| 6 | ESP32 controller | 5 W | Main control — reads sensors, switches loads |
| 7 | Temp / RH / PIR sensors | 5 W | Monitoring drying conditions and safety |
| 8 | Display | 3 W | Shows live status and readings |
| 9 | Buzzer, relays, LEDs | 5 W | Load switching, alerts, indication |
| 10 | Solar panel | 100 Wp | Primary (free) power source |
| 11 | Solar charge controller | 40 A | Battery protection and DC distribution |
| 12 | 24 V DC heater controller | — | Regulates solar power delivered to the heater |
| 13 | 24 V AC-DC supply | 600 W | Grid backup power for the heater |
| 14 | Battery | 12 V, 75 Ah | Backup for electronics and low-power loads |
| 15 | Inverter | 1 kVA | Small AC backup loads |
| 16 | Changeover switch, MCB, wiring | — | Source selection between solar/grid and protection |

## 5. Temperature — Normal (Open Sun) Drying Conditions

Reference values for how ambient conditions affect open-sun drying time, used to size the machine's target drying range:

| Conditions | Approx. temperature | Drying time |
|---|---|---|
| Weak sun / cloudy | 25–30°C | 1–2 days |
| Good sunny weather | 30–35°C | 6–10 hours |
| Strong dry sunlight + good airflow | 35–40°C | 4–8 hours |
| Very humid weather | 28–35°C | 1–2 days |

The proposed machine holds a controlled 35–40°C chamber temperature with forced airflow at all times (regardless of outside weather), which is why it consistently dries in 4–5 hours.

## 6. Comparison Charts

### 6.1 Drying Time — Regular vs Proposed Machine

![Drying time comparison](images/drying_time.png)

### 6.2 Packaging Output — Regular vs Proposed Machine

![Packaging output comparison](images/packaging_output.png)

## 7. Benefits

- Drying time cut from 1–2 days (open sun, weather-dependent) down to a consistent 4–5 hours.
- Works day or night, sun or rain, thanks to hybrid solar + grid power.
- Automatic tray-tilt hand-off removes manual lifting/unloading between drying and packaging.
- Consistent stick quality from controlled temperature and humidity.
- Roughly 2.5× the daily packaging output, since open-sun drying often can't complete a full batch within one working day.
- Low hardware cost (~Rs 18,200) with an estimated payback of about 3–4 weeks of operation.
- Reduces manual drudgery for home-based women artisans, freeing time for other work.

## 📁 Repository Structure

```
├── README.md          # this file
├── docs/               # slides, project report, calculations
├── images/              # prototype photos, diagrams, charts
├── hardware/            # component list, circuit diagram
└── code/                # ESP32 firmware
```
