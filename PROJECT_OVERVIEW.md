# Project Overview: Dune 3000 RTS Engine and Procedural Graphics (`dune3000`)

## Purpose and Scope

`dune3000` is a deterministic Real-Time Strategy (RTS) simulation engine, procedural SVG graphics generator, and self-contained browser skirmish game inspired by *Dune 2000*. It models economy, base construction, power grid efficiency, rock-paper-scissors combat multipliers, subterranean sandworm ecology, Coriolis weather fronts, Fremen Sietch diplomacy, and multi-personality AI commanders.

## Repository Structure

- [dune3000/engine.py](file:///botworkspace/dune3000/dune3000/engine.py): Core deterministic RTS simulation engine (`GameState`, `GridMap`, `Building`, `Unit`, `Sandworm`, `WeatherFront`, `compute_damage`).
- [dune3000/procgen.py](file:///botworkspace/dune3000/dune3000/procgen.py): Algorithmic SVG sprite generator (`generate_terrain_svg`, `generate_building_svg`, `generate_unit_svg`, `generate_sandworm_svg`, `generate_explosion_svg`, `generate_minimap_svg`).
- [dune3000/__init__.py](file:///botworkspace/dune3000/dune3000/__init__.py): Public package interface exporting all simulation classes, constants, and procedural rendering functions.
- [index.html](file:///botworkspace/dune3000/index.html): Self-contained interactive HTML5/Canvas browser game with HUD, production sidebar, radar minimap, audio synthesis, and AI skirmish loop.
- [tests/test_engine.py](file:///botworkspace/dune3000/tests/test_engine.py): Unit test suite covering all 40 gameplay mechanics, AI commander decisions, and SVG procedural generators.
- [tickets/](file:///botworkspace/dune3000/tickets/): 42 resolved engineering specification tickets (`ticket-001` through `ticket-040`).
- `assets/terrain/` and `images/dune2000_tiles_64/`: Tile and structure graphics assets (`64x64` PNG tileset).

## Core Mechanics Implemented in `dune3000/engine.py`

1. **Great Houses and Special Units**:
   - **Atreides**: `SonicTank` (long-range sonic wave artillery).
   - **Harkonnen**: `Devastator` (heavy dual-plasma siege armor).
   - **Ordos**: `Deviator` (nerve-gas missile launcher capable of temporary unit allegiance conversion).
2. **Base Economy and Infrastructure**:
   - **Power Grid**: `WindTrap` power output vs building consumption determines `power_efficiency()` (`0.25` to `1.0`).
   - **Concrete Foundations**: Buildings placed on `CONCRETE` avoid the 50% desert structural degradation penalty (`place_building`).
   - **Spice Harvesting and Silo Capacity**: `Harvester` units gather from `SPICE_THICK` and `SPICE_THIN` tiles; `Silo` and `Refinery` structures determine `max_spice_capacity()`; CHOAM `trade_spice()` and `order_starport_unit()` handle dynamic market pricing.
   - **Repair and Sell**: `repair_building()` restores structure HP for proportional credits; `sell_building()` refunds 50% of construction cost.
3. **Combat, Veterancy, and Tactical AI**:
   - **Damage Matrix (`compute_damage`)**: Evaluates weapon types (`bullet`, `shell`, `missile`) against armor classes (`infantry`, `light`, `heavy`, `building`).
   - **Veterancy (`gain_xp`)**: Units promote from `Rookie` to `Veteran` and `Elite`, gaining HP and attack bonuses.
   - **Tactical Behavior**: Includes kiting (`compute_kiting_step`), low-HP retreat (`retreat_towards`), target prioritization (`select_priority_target`), and flocking formation offsets (`compute_formation_offset`).
   - **AI Commander Personalities (`COMMANDER_PROFILES`)**: `MethodicalMentat`, `AggressiveRaider`, and `EconomicTurtler` drive `step_ai_commander()`.
4. **Arrakis Hazards and Special Operations**:
   - **Sandworm Ecology**: `Sandworm` tracks vibrations on sand/dunes (`step`) and executes subterranean ambushes (`step_sandworm_ambush`), while `Carryall` airlifts endangered harvesters (`step_carryall_rescue`).
   - **Coriolis Weather Fronts**: Moving `WeatherFront` objects (`spawn_weather_front`, `step_weather_fronts`, `apply_sandstorm`) obscure radar and damage exposed units on sand.
   - **Covert & Superweapon Actions**: `Engineer` building capture (`capture_building`), `Saboteur` stealth demolition (`sabotage`), Fremen Sietch infiltration (`infiltrate_sietch`), and Palace `Death Hand` missile strike (`fire_death_hand`).

## Running Verification

```bash
python3 -m unittest discover -s /botworkspace/dune3000/tests -p "test_*.py"
```
