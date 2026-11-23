# Blue Theater Agent Instructions

When working in this folder, treat `.agents/skills/` as project-local Agent Skills.

Before game-development work, read:

1. `README.md`
2. `.agents/skills/router/SKILL.md`

Use the router's progressive-disclosure rules: load only the engine, discipline, genre, and workflow skills needed for the current request. This is a Red Alert-like 2D naval RTS and Unity is the selected engine. Read `ProjectSettings/ProjectVersion.txt` before using engine APIs once the Unity project exists; do not substitute Godot APIs.

For naval movement and long-range pathfinding, use the grid, waypoint-graph, or flow-field techniques from `game-ai`. Do not assume Unity NavMesh works over the sea; use `unity-navmesh` only after confirming that the map model and navigation bake support the intended water lanes.

`tower-defense` is an economy/targeting reference, not a complete RTS template. Preserve the user's scope and validate gameplay behavior with runnable checks rather than relying on visual inspection alone.
