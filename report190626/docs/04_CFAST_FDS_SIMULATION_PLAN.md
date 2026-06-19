# 04 — CFAST/FDS Simulation Plan / Kế hoạch mô phỏng CFAST/FDS

## VI — Quyết định cuối cùng

| Engine | Vai trò |
|---|---|
| CFAST | nguồn sinh dataset chính cấp phòng/khu vực |
| FDS | kiểm chứng chi tiết một số case |
| AI | surrogate model dự đoán nhanh |
| Dashboard | trực quan hóa/replay/inference |

## EN — Final decision

| Engine | Role |
|---|---|
| CFAST | primary room/zone-level dataset generator |
| FDS | detailed validation for selected cases |
| AI | fast surrogate model |
| Dashboard | visualization/replay/inference |

---

## VI — CFAST là chính vì

- phù hợp cấp khoang/node;
- chạy nhanh hơn FDS;
- dễ chạy batch nhiều kịch bản;
- output phù hợp để tạo `smoke_label`, `arrival_time`, `temperature`, `layer_height`;
- phù hợp với thời gian 4–5 tháng.

## EN — CFAST is primary because

- suitable for compartment/node-level outputs;
- faster than FDS;
- easier for batch scenarios;
- outputs are suitable for `smoke_label`, `arrival_time`, `temperature`, `layer_height`;
- feasible within 4–5 months.

---

## VI — FDS không dùng toàn bộ vì

- mesh tòa 10–20 tầng quá lớn;
- chạy hàng trăm case là không khả thi;
- hậu xử lý field 3D phức tạp;
- dễ làm chậm toàn bộ đề tài;
- mục tiêu không phải CFD 3D toàn nhà.

## EN — FDS is not used for bulk dataset because

- mesh for a 10–20 floor building is too large;
- hundreds of FDS cases are infeasible;
- 3D field post-processing is complex;
- it may delay the entire project;
- the goal is not full-building 3D CFD.

---

## VI — Input CFAST

| Parameter | Source | Priority |
|---|---|---|
| Compartment dimensions | BIM/IFC | P0 |
| Floor/ceiling elevation | BIM/IFC | P0 |
| Horizontal vents | doors/windows/openings | P0 |
| Vertical vents | stairs/shafts | P1 |
| Mechanical vents | exhaust/pressurization scenario | P0/P1 |
| HRR curve | scenario/literature assumption | P0 |
| Fuel type | scenario/literature assumption | P0 |
| Soot yield | literature assumption | P0 |
| CO yield | literature assumption | P1 |
| Detector/sprinkler | scenario/system | P1 |
| Initial conditions | weather/assumption | P0 |
| Simulation duration | config | P0 |
| Output interval | config | P0 |

## EN — CFAST inputs

| Parameter | Source | Priority |
|---|---|---|
| Compartment dimensions | BIM/IFC | P0 |
| Floor/ceiling elevation | BIM/IFC | P0 |
| Horizontal vents | doors/windows/openings | P0 |
| Vertical vents | stairs/shafts | P1 |
| Mechanical vents | exhaust/pressurization scenario | P0/P1 |
| HRR curve | scenario/literature assumption | P0 |
| Fuel type | scenario/literature assumption | P0 |
| Soot yield | literature assumption | P0 |
| CO yield | literature assumption | P1 |
| Detector/sprinkler | scenario/system | P1 |
| Initial conditions | weather/assumption | P0 |
| Simulation duration | config | P0 |
| Output interval | config | P0 |

---

## VI — Output CFAST

| Output | Usage |
|---|---|
| Upper layer temperature | hazard/time-series |
| Lower layer temperature | sensor proxy |
| Smoke layer height | smoke/hazard proxy |
| Soot concentration | smoke label/visibility proxy |
| CO concentration | toxic hazard |
| Flow through vents | spread direction/path |
| Detector activation time | alarm simulation |
| Sprinkler activation time | system state |
| Pressure | stack/flow diagnostic |
| Arrival time | regression target |
| Smoke/no-smoke | classification target |

## EN — CFAST outputs

| Output | Usage |
|---|---|
| Upper layer temperature | hazard/time-series |
| Lower layer temperature | sensor proxy |
| Smoke layer height | smoke/hazard proxy |
| Soot concentration | smoke label/visibility proxy |
| CO concentration | toxic hazard |
| Flow through vents | spread direction/path |
| Detector activation time | alarm simulation |
| Sprinkler activation time | system state |
| Pressure | stack/flow diagnostic |
| Arrival time | regression target |
| Smoke/no-smoke | classification target |

---

## VI — FDS validation tier

| Tier | Number of cases | Meaning |
|---|---:|---|
| P0 | 3 | minimum validation |
| P1 | 6 | target validation level |
| P2 | 8–12 | only if time/hardware allows |

## EN — FDS validation tier

| Tier | Number of cases | Meaning |
|---|---:|---|
| P0 | 3 | minimum validation |
| P1 | 6 | target validation level |
| P2 | 8–12 | only if time/hardware allows |

---

## VI — FDS case candidates

| Case | Purpose |
|---|---|
| FDS-01 | Room → corridor |
| FDS-02 | Long corridor |
| FDS-03 | Room → corridor → stair |
| FDS-04 | Door open vs closed |
| FDS-05 | Window + wind |
| FDS-06 | Smoke exhaust off/on |
| FDS-07 | Stair pressurization off/on |
| FDS-08 | Sprinkler/no sprinkler or reduced HRR |

## EN — FDS case candidates

| Case | Purpose |
|---|---|
| FDS-01 | Room → corridor |
| FDS-02 | Long corridor |
| FDS-03 | Room → corridor → stair |
| FDS-04 | Door open vs closed |
| FDS-05 | Window + wind |
| FDS-06 | Smoke exhaust off/on |
| FDS-07 | Stair pressurization off/on |
| FDS-08 | Sprinkler/no sprinkler or reduced HRR |

---

## VI — Đánh giá mô phỏng

Không khẳng định mô phỏng đúng tuyệt đối. Chỉ chứng minh đủ tin cậy trong phạm vi nghiên cứu bằng:

1. Kiểm tra graph topology.
2. Kiểm tra input simulation.
3. Sanity check vật lý.
4. Chạy layout nhỏ trước.
5. So sánh CFAST–FDS node-level.
6. Sensitivity analysis.
7. Ghi rõ giới hạn.

## EN — Simulation evaluation

Do not claim absolute correctness. Demonstrate sufficient credibility within the research scope through:

1. Graph topology check.
2. Simulation input check.
3. Physical sanity check.
4. Small-layout tests first.
5. Node-level CFAST–FDS comparison.
6. Sensitivity analysis.
7. Explicit limitations.
