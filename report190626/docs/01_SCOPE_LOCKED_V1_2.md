# 01 — Locked Scope v1.2 / Phạm vi cố định v1.2

## VI — Scope statement

Phạm vi cuối cùng của đề tài:

> Xây dựng một prototype nghiên cứu dự đoán lan truyền khói cấp phòng/khu vực trong tòa nhà cao tầng dựa trên BIM/IFC, building graph, dữ liệu mô phỏng CFAST, một số kiểm chứng FDS, IoT giả lập 3 lớp, điều kiện biên và mô hình AI dạng graph-time-series. CFAST là nguồn sinh dataset chính, FDS là nguồn kiểm chứng chọn lọc, AI là surrogate model để dự đoán nhanh, dashboard là công cụ trực quan hóa/replay/inference. Prototype không thay thế CFD, không thay thế thiết kế hoặc thẩm duyệt PCCC, không điều khiển hệ thống thật và không đưa ra kết luận pháp lý.

## EN — Scope statement

The final project scope:

> Build a research prototype for room/zone-level smoke-spread prediction in high-rise buildings using BIM/IFC, building graphs, CFAST simulation data, selected FDS validation cases, three-layer virtual IoT, boundary conditions, and graph-time-series AI. CFAST is the main dataset generator, FDS is a selected validation source, AI is a surrogate model for fast prediction, and the dashboard is for visualization/replay/inference. The prototype does not replace CFD, fire-protection design, regulatory approval, real system control, or legal conclusions.

---

## VI — P0: bắt buộc

| Hạng mục | Mô tả |
|---|---|
| Revit/IFC | Export IFC từ file Revit thật |
| Low-rise debug layout | 1 layout đơn giản để test pipeline |
| Building graph | node/edge/mapping BIM ID |
| Cụm 3–5 tầng | mô phỏng quanh tầng cháy |
| CFAST dataset | nguồn dữ liệu chính |
| Post-processing | node time-series + labels |
| Virtual IoT | `physics_truth`, `virtual_sensor_clean`, `iot_noisy_stream` |
| Labels P0 | `smoke_label`, `arrival_time` |
| System state P0 | sprinkler/exhaust/pressurization ON/OFF |
| AI baselines | rule-based, ML/MLP |
| Graph/time model | GNN/Temporal GNN prototype |
| Dashboard | replay + graph + inference |
| Evaluation | metrics + splits + leakage checks |

## EN — P0: mandatory

| Item | Description |
|---|---|
| Revit/IFC | Export IFC from real Revit file |
| Low-rise debug layout | one simple layout for pipeline testing |
| Building graph | node/edge/BIM ID mapping |
| 3–5 floor cluster | simulate around fire floor |
| CFAST dataset | main data source |
| Post-processing | node time-series + labels |
| Virtual IoT | `physics_truth`, `virtual_sensor_clean`, `iot_noisy_stream` |
| P0 labels | `smoke_label`, `arrival_time` |
| P0 system state | sprinkler/exhaust/pressurization ON/OFF |
| AI baselines | rule-based, ML/MLP |
| Graph/time model | GNN/Temporal GNN prototype |
| Dashboard | replay + graph + inference |
| Evaluation | metrics + splits + leakage checks |

---

## VI — P1: nên làm

| Hạng mục | Mô tả |
|---|---|
| FDS validation | mục tiêu 6 case |
| Hazard/unsafe labels | nếu có tiêu chuẩn hoặc proxy rõ ràng |
| Wind/boundary features | `wind_speed`, `wind_dir_sin/cos`, `wind_effect` |
| CO sensor/hazard | nếu CFAST/FDS output ổn |
| System PCCC simplified | `exhaust_flow`, `stair_delta_p` đơn giản |
| IoT robustness presets | low/medium/faulty |
| Ablation study | Graph, Fire, IoT, Boundary, System, Full |
| Dashboard stream | WebSocket/SSE virtual IoT |

## EN — P1: recommended

| Item | Description |
|---|---|
| FDS validation | target 6 cases |
| Hazard/unsafe labels | if standards-backed or clearly marked proxy |
| Wind/boundary features | `wind_speed`, `wind_dir_sin/cos`, `wind_effect` |
| CO sensor/hazard | if CFAST/FDS outputs are reliable |
| Simplified PCCC systems | simplified `exhaust_flow`, `stair_delta_p` |
| IoT robustness presets | low/medium/faulty |
| Ablation study | Graph, Fire, IoT, Boundary, System, Full |
| Dashboard stream | WebSocket/SSE virtual IoT |

---

## VI — P2: để sau

| Hạng mục | Lý do |
|---|---|
| FDS 8–12 case | chỉ nếu đủ phần cứng/thời gian |
| FDS toàn bộ tòa | quá nặng |
| IoT thật | cần hardware và dữ liệu thật |
| Evacuation chi tiết | bài toán riêng |
| HVAC duct chi tiết | quá phức tạp |
| Atrium CFD chi tiết | cần FDS chuyên sâu |
| ASET/RSET đầy đủ | cần mô hình thoát nạn và ngưỡng chuẩn |
| Điều khiển hệ thống thật | ngoài phạm vi |

## EN — P2: future work

| Item | Reason |
|---|---|
| 8–12 FDS cases | only if hardware/time allows |
| Full-building FDS | too expensive |
| Real IoT | requires hardware and real data |
| Detailed evacuation | separate problem |
| Detailed HVAC duct | too complex |
| Detailed atrium CFD | requires specialized FDS work |
| Full ASET/RSET | requires evacuation model and standards-backed thresholds |
| Real system control | out of scope |

---

## VI — Quy tắc khóa phạm vi

- Không thêm P1 khi P0 chưa chạy end-to-end.
- Không thêm P2 trong giai đoạn triển khai chính.
- Nếu FDS quá nặng, giảm case FDS, không làm chậm AI/dashboard.
- Nếu IFC lỗi, được sửa graph bán thủ công nhưng phải log rõ.
- Nếu không có ngưỡng chuẩn, dùng proxy label và ghi rõ là proxy nghiên cứu.
- Không tuyên bố kết quả thay thế CFD/thẩm duyệt PCCC.

## EN — Scope locking rules

- Do not add P1 before P0 runs end-to-end.
- Do not add P2 during the main implementation phase.
- If FDS is too heavy, reduce FDS cases; do not delay AI/dashboard.
- If IFC is messy, manually correct the graph but log it clearly.
- If thresholds are not standards-backed, use proxy labels and mark them as research proxies.
- Do not claim the system replaces CFD or fire-safety approval.
