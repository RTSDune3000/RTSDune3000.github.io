See `/botworkspace/AGENTS.md` and `/botworkspace/FACTBOOK.md` first for workspace-wide rules and core facts.

# `dune3000` Repository Overview (`PROJECT.dev.md`)

`dune3000` is a deterministic Real-Time Strategy (RTS) simulation engine, procedural SVG graphics generator, and self-contained HTML5/Canvas browser skirmish game.

## Module Boundaries

- `dune3000/engine.py` — Deterministic RTS simulation engine (`GameState`, `GridMap`, `Building`, `Unit`, `Sandworm`, `WeatherFront`, `compute_damage`, `step_ai_commander`).
- `dune3000/procgen.py` — Procedural SVG sprite and minimap generator (`generate_terrain_svg`, `generate_building_svg`, `generate_unit_svg`, `generate_sandworm_svg`, `generate_explosion_svg`, `generate_minimap_svg`).
- `dune3000/__init__.py` — Public package interface re-exporting engine and procedural rendering symbols.
- `index.html` — Self-contained browser RTS skirmish interface, HUD, and canvas loop.
- `tests/test_engine.py` — Unit test suite covering simulation mechanics, AI commander decisions, and procedural SVG generation.

## Build and Verification Commands

- Run full unit test suite:
  `python3 -m unittest discover -s /botworkspace/dune3000/tests -p "test_*.py"`
- Check pre-flight dependencies before modifying shared engine symbols:
  `python3 /botworkspace/tools/blast_radius_analyzer.py <target>`
