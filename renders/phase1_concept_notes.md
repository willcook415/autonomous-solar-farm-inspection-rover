# Phase 1 – Initial Rover Concepts

These are the first-round chassis concepts for the Autonomous Solar Farm Inspection Rover.  
Dimensions are approximate and intended for initial exploration.

---

## Concept 1 – Tall Mast with 180° Cameras
- **Key Features:**
  - Tall mast provides high vantage point for cameras
  - Dual 180° cameras (front and rear) for wide coverage
  - Narrow 30 cm track width for navigating tight panel rows
  - 30 cm wheel diameter gives ~15 cm ground clearance
- **Trade-offs:**
  - Narrow stance reduces lateral stability, especially on uneven terrain
  - Tall mast increases risk of tipping if CG is high

---

## Concept 2 – Quadruped with 360° Camera
- **Key Features:**
  - 360° camera provides full situational awareness
  - Mechanical legs for high terrain adaptability
  - Compact frame: 50 cm height, 40 cm width
- **Trade-offs:**
  - Significantly more complex to simulate in ROS/Gazebo
  - Legged design may be overkill for relatively flat solar farm environment

---

## Concept 3 – Tank-Style Tracked Rover
- **Key Features:**
  - Wide 75 cm tracked base provides excellent stability
  - High traction on gravel, dirt, and wet terrain
  - One-directional front camera for inspection tasks
- **Trade-offs:**
  - Tracks are more challenging to model and simulate accurately
  - Wider frame reduces clearance margin in narrow panel rows

---

**Next Step:**  
From these three concepts, two will be downselected for further evaluation using feasibility scoring and dimensional checks before final envelope definition.
