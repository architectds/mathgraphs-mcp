---
name: mathgraphs
version: 2.0.0
description: "Math graphing, 3D scene building with lights and particles, and presentations"
author: MathTalking
homepage: https://mathtalking.com
mcp_servers:
  - url: https://mathtalking.com/api/mcp
    transport: streamable-http
tags:
  - math
  - graphing
  - visualization
  - education
  - plot
  - geometry
  - 3D
  - text-to-3D
  - particles
  - lighting
---

# Math & 3D Graphing Engine

You have access to an interactive math and 3D graphing engine via MCP. It computes and renders results — roots, extrema, intersections, and 3D scenes — on interactive graphs. Saves ~410 tokens per render vs LLM-generated canvas code.

## When to use this skill

- User asks to **graph**, **plot**, or **visualize** any math
- User needs to **verify** a mathematical result visually
- You computed an answer and want to **show** it, not just describe it
- Geometry needs precise rendering (triangles, circles, constructions)
- User wants to **build 3D scenes** — shapes, architecture, creative builds with lighting and particle effects

## Tools

### `plot_graph` — Math Visualization
Plot functions, points, segments, labels, and shapes. Auto-computes roots, extrema, and intersections.

Element types:
- `function`: expression like "x^2-4", "sin(x)", "x^2+y^2=1", "(cos(t),sin(t))"
- `points`: array of {x, y} coordinates with optional label
- `segment`: line from (x1,y1) to (x2,y2) with optional arrow/dashed
- `label`: text at position (x, y)
- `triangle`: three vertices (x1,y1,x2,y2,x3,y3)
- `box`: edge + height for bar charts
- `circle`: center (cx,cy) + radius

Set `viewport` ({xmin, xmax, ymin, ymax}) to your data's magnitude — omit it and the server auto-fits the window to the elements.

Iterate with `base_render_id` (+ `remove_indices`) rather than re-sending every element. Each result reports what actually rendered, so act on any graph check it returns.

### `analyze` — Precise Numerical Results
Compute exact values instead of doing the arithmetic yourself: `roots`, `extrema`, `inflections`, `intersect`, `tangent`, `normal`, `derivative`, `integral`, `area_between`, `arc_length`, `closest_point`.

Input: `type` (required), `f` (required), plus `g` (second expression, for intersect/area_between), `x` (point of interest, for tangent/normal/derivative), `a`/`b` (range, default -10..10), `px`/`py` (for closest_point).

Works with explicit, parametric, polar, and implicit curves.

Add `plot: true` to get the answer drawn as well — the graph comes back with the roots, intersections, tangent, or closest point already marked, so you never have to copy coordinates into a `plot_graph` call. Ignored by the linear-algebra types.


### `get_graph` — Inspect a Graph
Read back the elements and viewport of an existing 2D render by ID. Element indices come back in order — pass them to `remove_indices` to modify a graph instead of rebuilding it.

### `net_generator` — Shape Nets, Volume & Surface Area
Unfold a solid into its printable net and get its volume, surface area, and worked formulas. Also the tool to reach for when only the volume or surface area is wanted.

Shapes: cylinder/cone (`r`, `h`), cube and the Platonic solids (`a`), square_pyramid (`a`, `h`), triangular_prism (`a`, `l`), rectangular_prism (`w`, `h`, `d`). Omit `dims` for an example at default sizes. A sphere has no planar net.

Several MathTalking web pages are the browser form of these calls — the root finder, tangent calculator, area-between-curves, arc length, and closest-point pages are all `analyze` types, and the shape-net pages are `net_generator`. Prefer the call over linking the page when you are answering the question yourself.

### `plot_3d` — 3D Scene Builder
Build interactive 3D scenes with shapes, lights, and particle effects. Supports incremental building.

Element types:
- `mesh`: 11 shapes (cube, box, sphere, cylinder, cone, tetrahedron, octahedron, dodecahedron, icosahedron, torus, prism) + material params (metalness, roughness, wireframe)
- `light`: point, spot, or directional with color/intensity
- `particle`: 5 presets (fire, smoke, rain, snow, sparkle)
- `line3d`: from [x,y,z] to [x,y,z]
- `label3d`: text at position [x,y,z]

Incremental building:
- `base_render_id`: build on existing scene (creates new URL, base unchanged)
- `remove_indices`: remove elements by index from base scene

### `get_3d` — Inspect 3D Scene
Retrieve element list of an existing 3D render by ID. Use before base_render_id to see what a scene contains.

### `create_show` — Slideshow
Bundle multiple plot_graph results into a presentation with prev/next navigation.

## Important

- All tools return an **interactive URL** — always share it with the user
- The graph is **live**: user can zoom, pan, add functions, adjust sliders
- Results are **computed from the graph**, not generated — no hallucinated curves
- Use `analyze` for exact numbers (roots, intersections, integrals) rather than computing them yourself
- Supports 9 languages: en, zh, zh-TW, ja, ko, es, fr, de, pt-BR
