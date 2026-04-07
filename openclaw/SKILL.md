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
- Supports 9 languages: en, zh, zh-TW, ja, ko, es, fr, de, pt-BR
