# Phase 1 – Feasibility & Downselect

Purpose: compare initial rover concepts against project goals and decide which **two** move forward to detailed envelope definition.

## Scoring rubric (1–5)
- 1 = poor / risky / high effort
- 3 = acceptable / moderate effort
- 5 = excellent / low effort

**Weights (sum to 100):**
- Relevance to use-case ………………… 20
- Simulation complexity (lower = higher score) … 20
- Stability (gravel/dirt, 10° slope) ……………… 15
- Maneuverability / row fit (2–3 m spacing) …… 15
- Sensor vantage / coverage …………………… 10
- Implementation time (Phase 2–3) …………… 10
- Risk / unknowns (lower risk = higher score) … 10

**Final score** = Σ( score × weight ) / 5

---

## Quick rationale per criterion
- **Relevance:** How well it matches a ground rover inspecting solar panels.
- **Simulation complexity:** How painful it’ll be in CAD/FEA + Gazebo/ROS.
- **Stability:** CG/stance vs tipping and rough terrain.
- **Maneuverability:** Width/turning vs tight corridors and obstacles.
- **Sensor vantage:** Field of view and mounting practicality.
- **Implementation time:** How fast we can build/test the sim stack.
- **Risk:** Unproven bits, edge cases, or toolchain pain.

---

## Scoring table

| Concept | Relevance (20) | Sim Complexity (20) | Stability (15) | Maneuverability (15) | Sensor Vantage (10) | Implement Time (10) | Risk (10) | **Total /100** |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **1 – Tall mast, 4 wheels** | 4 | 5 | 2 | 5 | 4 | 5 | 3 | **81** |
| **2 – Quadruped, 360° cam** | 2 | 1 | 4 | 4 | 5 | 1 | 1 | **50** |
| **3 – Tracked (tank-style)** | 4 | 3 | 5 | 3 | 3 | 3 | 3 | **70** |

> Notes (edit these as you refine):
> - **C1**: Super sim-friendly; narrow base hurts stability—address with wider track or lower CG.
> - **C2**: Cool, but heavy complexity + risk for this project scope.
> - **C3**: Very stable and realistic terrain handling; tracks add sim overhead.

---

## Decision
**Downselect:** Concept 1 and Concept 3 proceed to envelope definition.  
**Rationale:** Highest overall feasibility and relevance with manageable complexity.  
**Actions:** Update Phase 1 issues for envelope, sensors, and drive layout **for C1 and C3 only**. Record dimensions & assumptions in the design log.

