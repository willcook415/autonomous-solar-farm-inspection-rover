# Requirements & Test Plan
*Project:* Autonomous Solar Farm Inspection Rover — Virtual Prototype & Simulation  
*Owner:* William Cook (willcook415)  
*Doc version:* 0.1  
*Last updated:* 2025-08-15

> Purpose: make Phase 1–4 measurable and repeatable. This file defines the core requirements (R1–R3) and the tests that verify them. Keep this in `/docs/requirements_tests.md`.

---

## 1) System Requirements (Phase 0 baseline)
**R1 – Mission Time & Safety**  
Complete a **50 m** inspection route that includes placed obstacles **in < 90 s**, with **0 collisions** and **no operator intervention**.

**R2 – Fault Detection**  
Detect and log **all simulated panel faults** (N markers in scene). **Recall = 100%** (no false negatives). Track precision for transparency (target ≥95%).

**R3 – Reliability / Uptime**  
Across **10 consecutive runs** under nominal conditions (same world, randomized seeds), achieve **≥ 95% successful missions** (a “success” = R1 met + 0 collisions + log saved).

> Stretch (optional later): energy use per metre, mean lateral error in corridor, max roll/pitch.

---

## 2) Verification Matrix (traceability)
| Req ID | Verification Method | Test Case IDs | Status |
|---|---|---|---|
| R1 | Test (timed course) | TC-01, TC-02 | Planned |
| R2 | Test (fault scenario) | TC-03 | Planned |
| R3 | Test (batch reliability) | TC-04 | Planned |

---

## 3) Test Cases (procedures & pass criteria)

### TC-01 — Baseline Time Trial (flat, no obstacles)
**Goal:** Establish nominal speed profile and validate timing pipeline.  
**Setup:** 50 m straight/curved path between panel rows (row spacing 2–3 m), flat terrain.  
**Procedure:**  
1. Load baseline world and spawn rover at Start.  
2. Start logging (bag/CSV).  
3. Command mission start; rover follows corridor to Finish.  
4. Save logs; compute total time.  
**Metrics logged:** `T_total`, `distance_m`, `collisions`, `interventions`.  
**Pass:** `T_total < 90 s`, `collisions = 0`, `interventions = 0`.  
**Notes:** Used mainly to tune cruise speed; not counted for R1 but required before TC-02.

---

### TC-02 — Obstacle Course (verification for R1)
**Goal:** Verify time + safety with static obstacles in corridor.  
**Setup:** Same 50 m route; place K obstacles (e.g., pallets/cones) forcing detours; nominal slope ≤10°.  
**Procedure:**  
1. Load obstacle world; start logging.  
2. Run mission autonomously end-to-end.  
3. Export run summary.  
**Metrics:** `T_total`, `collisions`, `min_clearance`, `path_length`, `interventions`.  
**Pass (R1):** `T_total < 90 s`, `collisions = 0`, `interventions = 0`.

---

### TC-03 — Fault Detection Scenario (verification for R2)
**Goal:** Confirm all simulated panel faults are detected and logged.  
**Setup:** Add **N fault markers** (e.g., textures/flags) at panels along the route; keep obstacles from TC-02.  
**Procedure:**  
1. Start mission with perception stack enabled.  
2. At each detection, write a log entry with `fault_id`, `panel_pose`, `timestamp`.  
3. After run, compare detections to ground truth list.  
**Metrics:** `N_gt`, `N_detected`, `false_negatives`, `false_positives`, `precision`, `recall`.  
**Pass (R2):** `recall = 1.0` (no missed faults). Precision target ≥0.95 (informational).

---

### TC-04 — Reliability Batch (verification for R3)
**Goal:** Measure mission success rate across seeds/runs.  
**Setup:** World from TC-02 + TC-03; vary random seed (spawn jitter, sensor noise).  
**Procedure:**  
1. Automate **10 runs** (seed 1…10).  
2. Aggregate each run’s `T_total`, `collisions`, `interventions`, `detections`.  
3. Compute success bool per run: `R1 pass AND collisions=0 AND interventions=0 AND log saved`.  
**Metrics:** `success_count`, `success_rate = success_count/10`.  
**Pass (R3):** `success_rate ≥ 0.95`.

---

## 4) Logging & Data Schema (minimum fields)
Store either **CSV** (one row per timestep) + a **run_summary.json**, or **rosbag** topics with a post-run exporter.

**Per-timestep (CSV or topic-derived):**  
`timestamp, x, y, theta, v_lin, v_ang, collision_flag, obstacle_dist_min, fault_detected_flag, fault_id, cpu_time_step`

**Run summary (per mission):**  
`run_id, seed, T_total, distance_m, path_length, avg_speed, collisions, interventions, N_gt_faults, N_detected, precision, recall, success_bool`

---

## 5) Files & Conventions
- Place this file at `/docs/requirements_tests.md`.  
- Ground truth lists live in `/docs/ground_truth/` (e.g., `faults_world_v1.json`).  
- Export run summaries into `/docs/test_results/YYYY-MM-DD/` with filenames `TC-XX_runYY.json` and `TC-XX_runYY.csv`.

---

## 6) Review & Sign-off Checklist
- [ ] R1 verified by TC-02 (attach results)  
- [ ] R2 verified by TC-03 (attach results)  
- [ ] R3 verified by TC-04 (attach results)  
- [ ] README “Results” section updated with a short table/plot  
- [ ] Demo video exported to `/videos` and linked in README

> Keep this doc short and living. When you change a requirement, bump the doc version and summarize the diff at the top.
