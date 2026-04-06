---
name: mathgraphs
version: 1.1.0
description: "Math graphing, statistics, 3D scene building, computation, and visualization engine"
author: MathTalking
homepage: https://mathtalking.com
mcp_servers:
  - url: https://mathtalking.com/api/mcp
    transport: streamable-http
tags:
  - math
  - graphing
  - statistics
  - visualization
  - education
  - plot
  - geometry
  - 3D
  - text-to-3D
---

# Math, Statistics & 3D Graphing Engine

You have access to an interactive math, statistics, and 3D graphing engine via MCP. It computes and renders results — roots, extrema, intersections, regression, hypothesis tests, and 3D scenes — on interactive graphs. Saves ~410 tokens per render vs LLM-generated canvas code.

## When to use this skill

- User asks to **graph**, **plot**, or **visualize** any math
- User needs to **verify** a mathematical result visually
- You computed an answer and want to **show** it, not just describe it
- Data needs statistical visualization (histogram, regression, distribution fit)
- Geometry needs precise rendering (triangles, circles, constructions)
- User wants to **build 3D scenes** — describe objects, architecture, abstract art

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

### `compute_stats` — Descriptive Statistics
Input: array of numbers. Returns mean, median, std, min, max, quartiles.

### `add_histogram` — Histogram
Input: array of numbers. Auto-bins and draws bars.

### `add_regression` — Regression
Input: array of {x,y} points. Fits linear/quadratic/exponential/power. Returns R².

### `fit_distribution` — Distribution Fitting
Input: array of numbers. Fits normal/uniform/exponential. Returns best fit.

### `test_hypothesis` — Hypothesis Test
Input: data groups + test type. Returns p-value with visual rejection region.

### `plot_3d` — 3D Scene Builder
Place meshes (cube, sphere, cylinder, cone, tetrahedron, torus, prism, etc.), lines, and labels in 3D space. Returns interactive URL with orbit controls.

Element types:
- `mesh`: shape + position [x,y,z] + rotation [rx,ry,rz] + color
- `line3d`: from [x,y,z] to [x,y,z]
- `label3d`: text at position [x,y,z]

### `create_show` — Slideshow
Bundle multiple plot_graph results into a presentation with prev/next navigation.

## Important

- All tools return an **interactive URL** — always share it with the user
- The graph is **live**: user can zoom, pan, add functions, adjust sliders
- Results are **computed from the graph**, not generated — no hallucinated curves
- Supports 9 languages: en, zh, zh-TW, ja, ko, es, fr, de, pt-BR
