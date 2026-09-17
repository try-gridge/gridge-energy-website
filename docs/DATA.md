# Live data

The Live Control section is not a mockup. It renders a real anonymized export from a
Gridge-monitored home, plus the grid fault log from the same period.

## Provenance

- **Source:** one residential Gridge installation with a hybrid inverter (grid, solar, battery,
  generator) and circuit-level monitoring.
- **Window:** 1–7 August 2026, per-minute resolution.
- **Anonymization:** household name, address, account identifiers and precise location removed
  before export. What remains is electrical measurement only.
- **Tariff:** ₹8/kWh, applied in the page to turn kW into the ₹/hr figures.

Treat both files as company data. Do not publish them beyond this site without approval.

## `data/siddique_series.json`

Time series of source and load readings. Each entry is one timestamped snapshot: power drawn from
or fed to grid, solar, battery and generator, plus the per-circuit load breakdown (hall AC, dish
washer, fridge, other circuits) and the household total.

The page also carries a trimmed `SNAPSHOTS` array inline in the logic class, so the first paint
has numbers before the fetch resolves. If you refresh the JSON, refresh that array too or the two
will disagree for a moment on load.

## `data/alarms.json`

Grid quality events logged during the same window — voltage and frequency excursions, with
timestamps and the inverter's recovery. One of these surfaces as the "Grid quality" insight line
under the Circuit Monitor.

## How the page selects what to show

1. On mount, the logic class finds the snapshot whose time of day is nearest the visitor's local
   clock, so an evening visitor sees an evening load curve.
2. It re-selects every 60 seconds.
3. Switching a circuit off with a tap subtracts that circuit's load and recomputes Total Active,
   the ₹/hr estimates, and the "largest load right now" insight.

## Refreshing with a newer export

1. Produce a new export in the same shape, anonymized the same way.
2. Replace `data/siddique_series.json` (and `data/alarms.json` if the alarm window moved).
3. Update the inline `SNAPSHOTS` array to match.
4. Update the window dates wherever they appear in copy.
5. Check the Circuit Monitor: circuit **names** come from the data, so a renamed circuit changes
   the visible labels and the insight text.
