# 05 — Scenario and Factor Matrix / Kịch bản và factor matrix

## VI — Phạm vi kịch bản

Prototype dùng:

- 1 file Revit thật làm tòa chính.
- 1 layout thấp tầng đơn giản để debug và test generalization.
- Cụm 3–5 tầng quanh tầng cháy:
  - tầng cháy;
  - 1–2 tầng trên;
  - 1–2 tầng dưới;
  - cầu thang/shaft nối các tầng.

## EN — Scenario scope

Prototype uses:

- one real Revit file as the main building;
- one simple low-rise layout for debugging/generalization;
- a 3–5 floor cluster around the fire floor:
  - fire floor;
  - 1–2 floors above;
  - 1–2 floors below;
  - stairs/shafts connecting them.

---

## VI — Factor P0

| Group | Factor | Variable |
|---|---|---|
| Geometry | room area/volume/height | `room_area`, `room_volume`, `ceiling_height` |
| Geometry | corridor/stair/shaft connectivity | `adjacency`, `is_vertical` |
| Openings | door/opening area and height | `opening_area`, `opening_height` |
| Openings | door state | `door_state` |
| Fire | fire node/floor | `fire_node`, `fire_floor` |
| Fire | HRR/growth/fuel/soot | `HRR(t)`, `growth_class`, `fuel_type`, `soot_yield` |
| Boundary | initial/outdoor temperature | `T_initial`, `T_out` |
| System | sprinkler/exhaust/pressurization ON/OFF | `sprinkler_state`, `exhaust_state`, `pressurization_state` |
| Simulation | duration/output interval | `t_end`, `dt_out` |
| Labels | smoke and arrival | `smoke_label`, `arrival_time` |

## EN — P0 factors

| Group | Factor | Variable |
|---|---|---|
| Geometry | room area/volume/height | `room_area`, `room_volume`, `ceiling_height` |
| Geometry | corridor/stair/shaft connectivity | `adjacency`, `is_vertical` |
| Openings | door/opening area and height | `opening_area`, `opening_height` |
| Openings | door state | `door_state` |
| Fire | fire node/floor | `fire_node`, `fire_floor` |
| Fire | HRR/growth/fuel/soot | `HRR(t)`, `growth_class`, `fuel_type`, `soot_yield` |
| Boundary | initial/outdoor temperature | `T_initial`, `T_out` |
| System | sprinkler/exhaust/pressurization ON/OFF | `sprinkler_state`, `exhaust_state`, `pressurization_state` |
| Simulation | duration/output interval | `t_end`, `dt_out` |
| Labels | smoke and arrival | `smoke_label`, `arrival_time` |

---

## VI — Factor P1

| Group | Factor | Variable |
|---|---|---|
| Wind | wind speed/direction | `wind_speed`, `wind_dir_sin`, `wind_dir_cos` |
| Window | window state/broken/open | `window_state` |
| Fire | CO yield | `CO_yield` |
| Sensor | CO sensor | `co_sensor(t)` |
| System | exhaust flow | `exhaust_flow` |
| System | stair pressure difference | `stair_delta_p` |
| Label | hazard/unsafe | `hazard_label`, `unsafe_time` |
| Edge | fire rating | `fire_rating` |
| Boundary | wind effect on facade | `wind_effect` |

## EN — P1 factors

| Group | Factor | Variable |
|---|---|---|
| Wind | wind speed/direction | `wind_speed`, `wind_dir_sin`, `wind_dir_cos` |
| Window | window state/broken/open | `window_state` |
| Fire | CO yield | `CO_yield` |
| Sensor | CO sensor | `co_sensor(t)` |
| System | exhaust flow | `exhaust_flow` |
| System | stair pressure difference | `stair_delta_p` |
| Label | hazard/unsafe | `hazard_label`, `unsafe_time` |
| Edge | fire rating | `fire_rating` |
| Boundary | wind effect on facade | `wind_effect` |

---

## VI — Factor P2

| Group | Factor | Reason |
|---|---|---|
| HVAC | duct path/damper/supply/return | too complex |
| Atrium | detailed large-space CFD | needs specialized FDS |
| Leakage | exact smoke leakage | requires data/testing |
| Real IoT | hardware sensors | unavailable |
| Evacuation | detailed occupant movement | separate topic |
| ASET/RSET full | full evacuation + tenability | future work |

## EN — P2 factors

| Group | Factor | Reason |
|---|---|---|
| HVAC | duct path/damper/supply/return | too complex |
| Atrium | detailed large-space CFD | needs specialized FDS |
| Leakage | exact smoke leakage | requires data/testing |
| Real IoT | hardware sensors | unavailable |
| Evacuation | detailed occupant movement | separate topic |
| ASET/RSET full | full evacuation + tenability | future work |

---

## VI — Scenario sampling rules

- Không lấy full Cartesian product.
- Không để số kịch bản nổ tổ hợp.
- Dùng scenario sampling có kiểm soát.
- Mỗi scenario phải có:
  - `scenario_id`;
  - `building_id`;
  - `layout_id`;
  - `fire_node`;
  - `fire_floor`;
  - `HRR_config`;
  - `door_state_config`;
  - `system_state_config`;
  - `boundary_config`;
  - `simulation_config`.

## EN — Scenario sampling rules

- Do not use full Cartesian product.
- Prevent combinatorial explosion.
- Use controlled scenario sampling.
- Each scenario must have:
  - `scenario_id`;
  - `building_id`;
  - `layout_id`;
  - `fire_node`;
  - `fire_floor`;
  - `HRR_config`;
  - `door_state_config`;
  - `system_state_config`;
  - `boundary_config`;
  - `simulation_config`.
