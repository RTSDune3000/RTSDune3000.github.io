# Dune 3000: Deterministic RTS Engine and Procedural Graphics Suite

`dune3000` is a deterministic Real-Time Strategy (RTS) game engine (`dune3000/engine.py`), procedural SVG sprite generator (`dune3000/procgen.py`), and playable browser game (`index.html`) inspired by *Dune 2000*.

See [PROJECT_OVERVIEW.md](file:///botworkspace/dune3000/PROJECT_OVERVIEW.md) for full architectural documentation.

## Features

- **Deterministic Simulation Engine ([dune3000/engine.py](file:///botworkspace/dune3000/dune3000/engine.py))**:
  - Grid terrain passability (`SAND`, `DUNES`, `ROCK`, `CONCRETE`, `SPICE_THIN`, `SPICE_THICK`) and Fog of War (`compute_visibility`).
  - WindTrap power efficiency, Concrete Slab structural integrity, Spice Silo storage bounds, and CHOAM Starport dynamic pricing.
  - Weapon-vs-armor multiplier matrix (`compute_damage`), unit veterancy promotions (`Rookie`, `Veteran`, `Elite`), tactical kiting, flocking formations, and target prioritization.
  - Great House special units (`SonicTank`, `Devastator`, `Deviator`), Palace Death Hand missile (`fire_death_hand`), Engineer capture (`capture_building`), Saboteur stealth demolition (`sabotage`), and Fremen Sietch infiltration (`infiltrate_sietch`).
  - Subterranean Sandworm hunting and ambush mechanics (`Sandworm`, `step_sandworm_ambush`), Carryall harvester rescue (`step_carryall_rescue`), and moving Coriolis weather fronts (`WeatherFront`, `step_weather_fronts`).
  - AI Skirmish Commanders (`MethodicalMentat`, `AggressiveRaider`, `EconomicTurtler`).
- **Procedural Graphics Generator ([dune3000/procgen.py](file:///botworkspace/dune3000/dune3000/procgen.py))**:
  - Zero-dependency deterministic SVG generation for terrain tiles, buildings, units, sandworms, multi-layer explosions, and radar minimaps.
- **Browser RTS Interface ([index.html](file:///botworkspace/dune3000/index.html))**:
  - Standalone HTML5 Canvas RTS skirmish mode with real-time sidebar production, minimap radar, and unit command controls.

## Verification

```bash
python3 -m unittest discover -s /botworkspace/dune3000/tests -p "test_*.py"
```
