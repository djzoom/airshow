# 飞行表演规划系统 / Air Show Planner

A browser-based flight-display planner. Configure a team, drag together a
sequence of action modules, and the system auto-flies the whole show from
takeoff through aerobatics to landing — multi-aircraft formation flight
with smoke trails and a per-plane task layer for breakaway maneuvers.

Built with Three.js (vendored locally), one HTML file, no build step.

## Features

- **3 ship presets** — 八一 J-10 · Thunderbirds F-16 · Frecce Tricolori MB-339
- **8 formations** — TRAIL / LINE / V / DIAMOND / ARROW / ECHELON_R / ECHELON_L / BOX
- **12 action modules** — TAKEOFF / CLIMB / CRUISE / FORMATION_CHANGE /
  LOOP / BARREL_ROLL / BOMB_BURST / REGROUP / MIRROR_PASS / LOW_PASS /
  HIGH_PASS / BREAK_LANDING
- **6 per-plane tasks** — SOLO_LOOP / SOLO_ROLL / BREAK_LEFT / BREAK_RIGHT /
  CLIMB_OUT / DIVE, scheduled on absolute time windows that override the
  formation pursuit and rejoin automatically afterwards
- **4 cameras** — AUTO orbital / LEADER chase / GROUND spectator / WIDE establishing
- Full timeline with module ticks and per-aircraft task strips, scrub-able
- Generated plan text dump (team, modules, schedule, per-plane tasks)

## Run locally

```
git clone https://github.com/djzoom/airshow.git
cd airshow
python3 -m http.server 8080
```
Open <http://127.0.0.1:8080/>.

No npm install or build step. `vendor/three/` is committed so the page
boots without a CDN.

## Aircraft model credits (CC-BY)

The three preset airframes ship in this repo as vendored GLBs. Each is
licensed under Creative Commons Attribution and the original creator
must be credited:

| Preset | Model | Author | Source |
|---|---|---|---|
| 八一 / Bayi | `j10.glb` | **andertan** | [Sketchfab](https://sketchfab.com/3d-models/chengdu-j10-vigorous-dragon-3a1a1863e9ba44e88d35da0d5f23caeb) |
| Thunderbirds | `f16.glb` (extracted from a 6-jet collection) | **bohmerang** | [Sketchfab](https://sketchfab.com/3d-models/free-fighter-jet-collection-low-poly-cb5966c988d9403895be89b364c2252f) |
| Frecce Tricolori | `mb339.glb` | **helijah** | [Sketchfab](https://sketchfab.com/3d-models/aermacchi-mb-339-ab6694051fd04111a1b578b43909e604) |
| (legacy) | `b738.glb` | — | inherited from the MU5735 reconstruction repo |

If you republish derivatives, retain these attributions.

## Project layout

```
.
├── index.html             — entire app (UI + sim + render)
├── b738.glb               — Boeing 737, legacy fallback
├── j10.glb                — Chengdu J-10
├── f16.glb                — F-16 Fighting Falcon (extracted from collection)
├── mb339.glb              — Aermacchi MB-339
├── vendor/
│   └── three/             — Three.js r164 (core + GLTFLoader)
└── README.md
```

## License

Code: MIT.
3D models: CC-BY (see Aircraft model credits above).
