# Agent Docs v1.2 — PCCC Smoke Digital Twin Prototype

## VI — Mục đích

Bộ tài liệu này dùng để đưa cho coding/research agent đọc trước khi triển khai đề tài:

**Số hóa lan truyền khói trong tòa nhà dựa trên BIM/IFC, CFAST/FDS, IoT giả lập, điều kiện biên và học sâu dạng graph-time-series.**

Agent phải hiểu rằng đây là **prototype nghiên cứu**, không phải phần mềm thẩm duyệt PCCC, không phải hệ thống điều khiển PCCC thật, và không thay thế CFD.

## EN — Purpose

This documentation pack is intended for a coding/research agent before implementing the project:

**Digitalizing smoke spread in buildings using BIM/IFC, CFAST/FDS, virtual IoT, boundary conditions, and graph-time-series deep learning.**

The agent must understand that this is a **research prototype**, not a fire-safety approval tool, not a real fire-protection control system, and not a replacement for CFD.

---

## VI — Thứ tự đọc bắt buộc

1. `00_MASTER_CONTEXT.md`
2. `01_SCOPE_LOCKED_V1_2.md`
3. `02_PIPELINE_ARCHITECTURE.md`
4. `03_BIM_IFC_GRAPH_PLAN.md`
5. `04_CFAST_FDS_SIMULATION_PLAN.md`
6. `05_SCENARIO_AND_FACTOR_MATRIX.md`
7. `06_VIRTUAL_IOT_DATASET_PLAN.md`
8. `07_AI_MODEL_EVALUATION_PLAN.md`
9. `08_DASHBOARD_PROTOTYPE_PLAN.md`
10. `09_STANDARDS_AND_LIMITATIONS.md`
11. `10_IMPLEMENTATION_ROADMAP.md`
12. `11_AGENT_OPERATING_RULES.md`
13. `12_ACCEPTANCE_CHECKLIST.md`

## EN — Required reading order

1. `00_MASTER_CONTEXT.md`
2. `01_SCOPE_LOCKED_V1_2.md`
3. `02_PIPELINE_ARCHITECTURE.md`
4. `03_BIM_IFC_GRAPH_PLAN.md`
5. `04_CFAST_FDS_SIMULATION_PLAN.md`
6. `05_SCENARIO_AND_FACTOR_MATRIX.md`
7. `06_VIRTUAL_IOT_DATASET_PLAN.md`
8. `07_AI_MODEL_EVALUATION_PLAN.md`
9. `08_DASHBOARD_PROTOTYPE_PLAN.md`
10. `09_STANDARDS_AND_LIMITATIONS.md`
11. `10_IMPLEMENTATION_ROADMAP.md`
12. `11_AGENT_OPERATING_RULES.md`
13. `12_ACCEPTANCE_CHECKLIST.md`

---

## VI — Quyết định lõi đã chốt

- Dùng **1 file Revit thật** làm tòa chính.
- Thêm **1 layout thấp tầng đơn giản** để debug và test generalization.
- Với tòa 10–20 tầng, chỉ mô phỏng **cụm 3–5 tầng quanh tầng cháy** trong prototype.
- **CFAST** là nguồn sinh dataset chính.
- **FDS** dùng kiểm chứng chọn lọc:
  - P0: 3 case.
  - P1: 6 case.
  - P2: 8–12 case nếu còn thời gian/phần cứng.
- IoT dùng mô hình 3 lớp:
  - `physics_truth`
  - `virtual_sensor_clean`
  - `iot_noisy_stream`
- Sprinkler, hút khói, tăng áp cầu thang:
  - P0: trạng thái ON/OFF.
  - P1: thêm flow/pressure đơn giản.
- AI đi theo lộ trình baseline trước, GNN sau.
- Dashboard chỉ replay/inference/stream IoT giả lập.
- Realtime chỉ ở AI/dashboard, không realtime CFD.

## EN — Locked core decisions

- Use **one real Revit file** as the main building.
- Add **one simple low-rise layout** for debugging and generalization testing.
- For the 10–20 floor building, simulate only a **3–5 floor cluster around the fire floor** in the prototype.
- **CFAST** is the primary dataset generator.
- **FDS** is used for selected validation:
  - P0: 3 cases.
  - P1: 6 cases.
  - P2: 8–12 cases if time/hardware allows.
- IoT uses three data layers:
  - `physics_truth`
  - `virtual_sensor_clean`
  - `iot_noisy_stream`
- Sprinkler, smoke exhaust, stair pressurization:
  - P0: ON/OFF state.
  - P1: simplified flow/pressure.
- AI must follow baselines first, then GNN.
- Dashboard only supports replay/inference/virtual IoT streaming.
- Real-time applies only to AI/dashboard, not CFD.
