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

A compact, wheeled machine that combines stick drying and packaging in a single unit, powered by a solar + 230 V grid supply so it can run in sunlight, at night, and in bad weather.



**Core idea:**

- Sticks are loaded onto removable stainless-steel mesh trays inside an enclosed drying chamber.
- A positive temperature coefficient ( PTC ) heater dry the sticks in 4–5 hours instead of the 1–2 days open-sun drying can take.
- Once dry, each tray tilts automatically and slides the sticks move into the packaging section — removing manual unloading.
- An ESP32 microcontroller reads temperature/humidity/IR sensors and automatically switches the heater and Exhaust fans 
- Power comes from a 500 Wp solar panel with battery backup, switching automatically to the 230 V grid when solar is insufficient.

## 3. Technical Approach

### 3.1 Drying Chamber — Mesh Tray & Tilting Design

The drying chamber holds 3 removable stainless-steel mesh trays stacked in a rack, each independently reachable by the hot-air stream from the heater 

| Parameter | Specification (indicative design values) |
|---|---|
| Tray size | 600 mm (L) × 400 mm (W) × 50 mm (deep)  ( Styrofoam insulation )|
| Mesh opening | 3 mm × 3 mm woven stainless-steel mesh — holds stick base upright while allowing hot air through |
| Trays per unit | 3 trays, stacked with ~60 mm gap between them for airflow |
| Sticks per tray | ≈ 300 sticks per tray, arranged upright in slotted mesh rows |
| Sticks per drying cycle | ≈ 900 sticks (3 trays) = one 1 kg batch, matching 18 packets of 50 g (50 sticks each) |
| Tilting mechanism | Small motor/servo tilts each tray to ~40–45° after the drying cycle ends |
| Unloading | Tilted tray slides dried sticks directly a chute directly to the counting/packaging system |
| Drying time per cycle | 4–5 hours (vs 1–2 days in open sun drying, weather-dependent) |

This tray-and-tilt design is what lets the same unit handle both drying and the hand-off into packaging, without a person manually lifting or emptying trays.

### 3.2 Solar Panel

| Parameter | Specification (typical 100 Wp panel) |
|---|---|
| Rated power | 500 Wp (polycrystalline/monocrystalline) |
| Panel size | ≈ 1000 mm (L) × 670 mm (W) × 30 mm (D) |
| Weight | ≈ 10-15 kg |
| Mounting | Fixed tilt frame, ~20–30° facing south, on top of or beside the machine cabinet |
| Output | Charge controller (40 A) → battery (12 V, 150 Ah) + heater controller 



### 3.3 Smart Control (ESP32)

```
Sensors (Temperature, Humidity, Moisture) → ESP32 → Relays (heater, fans) + Display + Buzzer/LEDs
```

The ESP32 continuously reads chamber temperature and humidity and switches the heater/fan relays to hold the target drying range.

### 3.4 Packaging System

Dried sticks slide off the tilted tray onto a short feed that leads into the packaging section, where bundling, weighing/counting and sealing happen in sequence.

| Parameter | Specification (indicative design values) |
|---|---|
| Counting | IR sensor for stick counter
| Pouch | Pre-formed LDPE/BOPP poly pouch, ≈ 230 mm (L) × 70 mm (W) — sized for standard 9-inch (≈230 mm) agarbatti sticks bundled together |
| Sealing method | Impulse heat sealer, 100 W, ~150–180°C sealing temperature, 5 s seal time per packet |
| Packaging cycle | ≈ 40–45 s per packet (count → bundle → feed → seal) |
| Output per batch | 18 packets per 50 -stick (1 kg) drying batch |
| Output per day | ≈ 54 packets across a 12-hour working day (3 batches) |
| Collection | Sealed packets drop onto a small output tray/bin for manual pickup |

This keeps packaging automatic: the machine handles counting, wrapping and sealing

## 4. Components List


| # | Component | Rating | Cost (Rs) | Why it's used |
|---|---|---|---|---|
| 1 | solar panel | 500 W | 10,000 | Primary (free) power source |
| 2 | DC circulation/exhaust fans | 80 W | 500 | Air circulation and moisture removal from the chamber |
| 3 | Packaging / sealing unit | 100 W | 700 | wrapping and packing |
| 4 | ESP32 controller | 5 W | 450 | Main control — reads sensors, switches loads |
| 5 | Temp / Humidity/ moisture | 5 W | 500 | Monitoring drying conditions and safety |
| 6 | Display | 0.49W | 300 | Shows live status and readings |
| 7 | Buzzer, relays, LEDs | 5 W | 250 | Load switching, alerts, indication |
| 8 | DC-DC converter | - | 200 |
| 9 | charge controller | 40A | 900 | Battery protection and DC distribution |
| 10 | 24 V DC PTC heater fan | 240W | 600 | heated air will be circulated |
| 11 | Single phase supply | 230V supply | electricity bill | Grid backup |
| 12 | Battery | 12 V, 150Ah | 10,000| Backup for electronics and low-power loads |
| 13 | Changeover switch, MCB, wiring | — | 700 | Source selection between solar/grid and protection |
| 14 | SMPS rectifier | 12V 30A | 2000 | AC-DC |
| 15 | IR sensor | - | 100 | counting the sticks |
| 16 | Servomotor | - | 100-200 | tilting the trays |
| 17 | 3 Trays | - | 900 |
| | **TOTAL** | | **30,000** |
### 4.1 Drying system
<img width="1599" height="901" alt="WhatsApp Image 2026-09-29 at 1 43 15 PM" src="https://github.com/user-attachments/assets/a52e627b-0adb-4bbe-b022-52be2261c9c5" />


## 4.2 overview of components
<img width="1536" height="1024" alt="WhatsApp Image 2026-09-28 at 6 18 58 PM" src="https://github.com/user-attachments/assets/077d385f-aee4-4eae-a023-bdd11e2dafca" />






## 5. Temperature — Normal (Open Sun) Drying Conditions

Reference values for how ambient conditions affect open-sun drying time, used to size the machine's target drying range:

| Conditions | Approx. temperature | Drying time |
|---|---|---|
| Weak sun / cloudy | 25–30°C | 1–2 days |
| Good sunny weather | 30–35°C | 6–10 hours |
| Strong dry sunlight + good airflow | 35–40°C | 4–8 hours |
| Very humid weather | 28–35°C | 1–2 days |

The proposed machine holds a controlled 45-50°C chamber temperature with forced airflow at all times (regardless of outside weather), which is why it consistently dries in 4–5 hours.

### 5.1 Our Machine — Drying Conditions (for comparison)

Unlike open-sun drying, the machine's chamber temperature and drying time stay the same no matter what the power source or outside weather is:

| Power source / condition | Chamber temperature | Drying time |
|---|---|---|
| Sunny day (solar direct) | 35–40°C | 4–5 hours |
| Cloudy day (battery backup) | 35–40 degree celcius | 4–5 hours | 
| Night / rainy day (grid backup) | 35–40°C | 4–5 hours |

## 6. Comparison Charts & Data

### 6.1 Drying Time — Regular vs Proposed Machine

![Drying time comparison]
<img width="1080" height="720" alt="WhatsApp Image 2026-09-28 at 8 59 07 AM" src="https://github.com/user-attachments/assets/6d8940a8-8875-4c57-9624-639d9a5c8dab" />


| Method | Drying time |
|---|---|
| Regular open-sun drying | 1–2 days (weather-dependent) |
| Proposed machine | 4–5 hours (consistent, any weather/time) |

### 6.2 Packaging Output — Regular vs Proposed Machine

![Packaging output comparison]
<img width="1200" height="1600" alt="WhatsApp Image 2026-09-28 at 10 14 07 AM" src="https://github.com/user-attachments/assets/62003489-2c6f-4f14-ad56-43313cb86cba" />



| Method | 50 g packets produced per day |
|---|---|
| Regular (hand packing) | ≈ 4.5 packets/day |
| Proposed machine | ≈ 18 packets/day |

## 7. Benefits

- Drying time cut from 1–2 days (open sun, weather-dependent) down to a consistent 4–5 hours.
- Works day or night, sun or rain, by using solar + grid power.
- Automatic tray-tilt hand-off removes manual lifting/unloading between drying and packaging.
- Consistent stick quality from controlled temperature and humidity.
- Roughly the daily packaging output, since open-sun drying often can't complete a full batch within one working day.
- Low hardware cost (~Rs 30,000) with an estimated payback of about 3–4 weeks of operation.
- Reduces manual drudgery for home-based women artisans, freeing time for other work.


