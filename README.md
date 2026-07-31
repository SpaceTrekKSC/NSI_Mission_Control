# NSI® Mission Control

**NSI® Mission Control** is the desktop application for flying a **Near Space Investigation® (NSI)** high‑altitude balloon mission end to end — plan it, fly it, track it, and recover it — from one program that works **completely offline in the field**.

Developed by **Atlantis Educational Services, Inc.** for the **Near Space Investigation®** program, it replaces the legacy LabVIEW "NSI Data Display" with a single cross‑platform app that plans the flight, receives and records live telemetry from the NSI Flight Computer (relayed by the Ground Station over the 900 MHz XBee SX link), predicts where the balloon will land, and manages the NSI hardware over USB. Internet is only ever needed *ahead* of launch day — to download offline maps and wind data — and is never required at the launch site.

---

## Highlights

- **Plan any mission end to end** — weather go/no‑go, FAA Part 101 exempt check, gas & lift worksheet, flight prediction, NOTAM paperwork, checklist and crew roles — printed as one Mission Pack.
- **Live telemetry** from the 73‑field NSI stream, on a purpose‑built dashboard: gauges, attitude, GPS, radiation/UV, battery, and three student PODs.
- **Offline vector maps** with the live flight track, ground‑station marker, and a Monte‑Carlo landing zone that keeps tightening all the way down.
- **Flight prediction that runs inside the app** on every platform — the offline ASTRA Monte‑Carlo predictor and an optional online SondeHub source.
- **Device management over USB** — download flight logs from the Flight Computer's SD card, set the XBee radio pairing, and **update device firmware** with verification.
- **Everything is recorded automatically** (raw + CSV) and any session **replays** through the full pipeline.
- **Runs everywhere** — Windows, macOS (Apple Silicon & Intel), Linux, and Raspberry Pi 4/5 — and lets you know when a new version is out (installing it automatically on Windows).

---

## Plan the mission — Mission Planner

A complete pre‑flight workspace. Each plan is its own `.nsimission` file (auto‑named with the launch date), saved in a library you can reopen, duplicate and print.

- **Launch site & timing** — set the site by clicking the map (or type lat/lon, or use the GS position); ground elevation auto‑fills. Plan **months** ahead — the app marks predictions as approximate until inside the 7‑day forecast horizon, then sharpens automatically.
- **Launch‑day weather** — National Weather Service forecast for the site, scored **GO / CAUTION / NO‑GO** against the HAB go/no‑go criteria (cloud, visibility, surface wind), with alerts and sunrise/sunset. Cached in the mission file so the field laptop shows it offline.
- **Payload & FAA compliance** — list everything that flies; the card continuously checks the **FAA Part 101 exempt rules** (14 CFR §101.1(a)(4): package weight, the 3 oz/in² density rule, combined weight, ≤ 50 lb weak link) and reads **EXEMPT** only when every rule passes.
- **Gas & Lift worksheet** — from balloon, gas, neck lift and parachute it computes free lift, ascent/descent rate, burst altitude, time to burst, **helium volume and tanks to order**, fill diameter, and the launch→burst diameter range the FAA asks for.
- **Launch‑window sweep** — simulate a launch **every hour** across your window and drop a color‑coded landing dot per hour on the map; pick the safest hour and adopt it with one click.
- **NOTAM & FAA notification** — entirely offline, the planner finds the nearest airfields and ARTCC (magnetic radials via the current World Magnetic Model) and generates a **Leidos phone script** and a **courtesy‑notice email**, tracks your filing windows, and stores the NOTAM number.
- **Checklist, crew roles & Mission Pack** — the full HAB field checklist and role assignments save with the plan, and **Mission Pack** prints the entire plan (brief, weather, compliance, gas, NOTAM, roles, checklist) to PDF.
- **▶ Fly Mission** hands the plan's balloon, gas, payload and site to the live engine and attaches the flight recording to the same file — the plan you built becomes the record of the flight you flew.

## Fly it — live dashboard & telemetry

- **Link banner** tells you at a glance what's on the wire: 🟢 RECEIVING · 🟡 NO FC (GS alive, no Flight Computer) · 🔴 SILENT · ⚪ Disconnected — with packet, heartbeat and malformed counters and **GPS‑fix badges** for both units.
- **Dashboard** — Ground Station status, **recommended antenna orientation** (geodetic bearing, elevation and distance to the balloon), mission/GPS time, a live map with an altitude ticker, altitude‑vs‑temp and altitude‑vs‑time charts, and a gauge strip: packets/min, pressure, external/IR/payload temperatures, humidity, **UV index** (WHO color scale) and battery.
- **Flight data** — live ascent rate, **max ascent/descent**, and a **burst altitude** that appears only once burst is actually detected; **IMU** pitch/roll/yaw (BNO055); and a **PODS** panel with one LED per student pod (green = delivering data).
- **Graphs** — full‑resolution plotting of the seven core channels, vs Time or vs Altitude, with min/max stats and a color‑coded **raw data console** and send box.
- **Pods** — all three PODs, ten channels each, with per‑pod graphs.
- **Sensor‑fault aware** — `NAN` shows as **FAULT**, all‑zero GPS shows as **NO FIX** (never a false 0°N/0°E), and the values are still kept in the logs.
- **Field‑ready themes** — Dark, Light and a **High Contrast** theme built for direct sunlight; resizable, remembered layout.
- **No hardware?** A built‑in **Demo flight simulator** exercises every feature, including fix loss, a sensor fault and an RF dropout.

## See it — offline maps & prediction

- **Offline vector maps** — download map areas (up to a **500 km** radius) before launch day; no internet needed in the chase vehicle. Import `.pmtiles` maps, switch Dark/Light/High‑Contrast map styles, **Follow** the balloon or **Fit** the whole track, and **export the 3‑D track to KML** for Google Earth.
- **Flight prediction** — the **ASTRA offline Monte‑Carlo** predictor runs entirely inside the app (download winds once, ~2 MB), re‑predicting **every ~45 s** from the balloon's live position and measured rates; after burst it switches to a descent‑only simulation so the landing zone tightens all the way down. Every simulated landing draws as a **purple dot** so you can plan the recovery around the zone, not just the pin. An optional **SondeHub** online source is also available. *(ASTRA physics © University of Southampton, BSD‑3‑Clause.)*

## Manage your devices — Device Setup

Talks to the Flight Computer or Ground Station over its **own USB cable**, independent of the live telemetry connection (you can stream on one port and service a device on another).

- **SD‑card flight logs** (Flight Computer) — list, and **download every file checksum‑verified** (a mismatch is caught and the partial file removed); download all at once; delete with confirmation. The active log is protected from deletion.
- **XBee SX radio pairing** (both units) — set the shared **Network ID** and **Preamble**, written to the radio, **read back to verify**, then saved — a half‑programmed radio is impossible. A one‑click **"Set to match"** pairs the second unit, and each board re‑heals its radio to the saved pairing on every boot.
- **Firmware updates** — flash the connected Flight Computer or Ground Station to the latest **verified** firmware (downloaded from the official release page), with post‑flash verification and a **recovery‑flash** fallback if a board is ever left blank.

## Record, replay & keep your data

Every session is recorded automatically to a **raw log** (every byte as received — the authoritative record) and a **session CSV** (parsed, timestamped). **Replay** any past session — or a processed flight CSV — back through the entire live pipeline (dashboard, charts, map, pods), with every time axis driven by the GPS timestamps in the data. Export the current session to CSV, and the flight track to KML, anytime.

---

## Download & install

| Platform | Installer |
|---|---|
| **Windows 10/11** (64‑bit) | `NSI-Mission-Control-Setup-1.0.0.exe` |
| **macOS — Apple Silicon** | `NSI-Mission-Control-1.0.0-arm64.dmg` |
| **macOS — Intel** | `NSI-Mission-Control-1.0.0.dmg` |
| **Linux x64** | `NSI-Mission-Control-1.0.0.AppImage` · `nsi-mission-control_1.0.0_amd64.deb` |
| **Linux arm64 / Raspberry Pi 4/5** (64‑bit OS) | `NSI-Mission-Control-1.0.0-arm64.AppImage` · `nsi-mission-control_1.0.0_arm64.deb` |

**First‑launch security prompts** (these builds are not yet code‑signed):
- **Windows:** SmartScreen → **More info** → **Run anyway**.
- **macOS:** right‑click (Control‑click) the app → **Open** → **Open**. Once only.
- **Linux (.AppImage):** `chmod +x` then run. **(.deb):** `sudo apt install ./<file>.deb` — adds you to the `dialout` group for serial access (log out/in once).

**Serial notes:** on Windows install the **FTDI VCP** driver if no port appears; on Linux remove `brltty` if it grabs your USB serial adapter. On **Windows** the app downloads and installs new releases automatically; on **macOS and Linux** it checks for updates and opens the download page for the new version. Recommended device firmware: Flight Computer **v0.4.1+** (v0.4.2+ for radio pairing), Ground Station **v3.3.0+** — older firmware still streams telemetry; the Device Setup features need these.

---

## The NSI telemetry stream (reference)

One CSV line every ~12 s at 115200 baud, **73 fields**: GPS date/time, flight GPS (position/altitude/speed), atmosphere (humidity, temperature, pressure), IMU (attitude, accel, mag), radiation (IR temp, UV), battery, **three POD blocks of 10 channels each** (prefixed by a pod‑ID marker), and the Ground Station's own GPS/temperature/pressure. `NAN` = sensor fault; an all‑zero GPS block = no fix.

---

## Credits & license

Developed by **Atlantis Educational Services, Inc.** for the **Near Space Investigation®** program.
© 2026 Atlantis Educational Services, Inc. All rights reserved.
Flight prediction adapted from the **ASTRA** simulator (University of Southampton, BSD‑3‑Clause).
