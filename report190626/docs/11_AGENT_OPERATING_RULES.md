# 11 — Agent Operating Rules / Quy tắc vận hành cho Agent

## VI — Nguyên tắc làm việc

1. Luôn đọc `01_SCOPE_LOCKED_V1_2.md` trước khi code.
2. Không tự ý mở rộng scope.
3. Không thêm P1 nếu P0 chưa chạy end-to-end.
4. Không thêm P2 nếu chưa được yêu cầu.
5. Không bịa thông số PCCC.
6. Không tự đặt ngưỡng hazard như kết luận pháp lý.
7. Nếu dùng ngưỡng proxy, ghi rõ là `research proxy`.
8. Luôn chống label leakage.
9. Luôn lưu raw output và processed output riêng.
10. Luôn log assumptions và manual fixes.
11. Luôn có baseline trước GNN.
12. Dashboard phải trace được dữ liệu về pipeline.

## EN — Working principles

1. Always read `01_SCOPE_LOCKED_V1_2.md` before coding.
2. Do not expand scope on your own.
3. Do not add P1 before P0 runs end-to-end.
4. Do not add P2 unless explicitly requested.
5. Do not fabricate fire-safety parameters.
6. Do not set hazard thresholds as legal conclusions.
7. If using proxy thresholds, mark them as `research proxy`.
8. Always prevent label leakage.
9. Always separate raw and processed outputs.
10. Always log assumptions and manual fixes.
11. Always build baselines before GNN.
12. Dashboard data must be traceable to the pipeline.

---

## VI — Khi thiếu dữ liệu

Nếu thiếu dữ liệu:

1. Ghi rõ dữ liệu thiếu.
2. Đưa giả định tối giản.
3. Lưu giả định vào config/log.
4. Không biến giả định thành sự thật.
5. Ưu tiên chạy end-to-end.
6. Đưa phần thiếu vào `limitations.md`.

## EN — When data is missing

If data is missing:

1. State what is missing.
2. Use the simplest reasonable assumption.
3. Save the assumption in config/log.
4. Do not turn assumptions into facts.
5. Prioritize end-to-end execution.
6. Add missing parts to `limitations.md`.

---

## VI — Không được làm

| Forbidden | Reason |
|---|---|
| full-building FDS for hundreds of cases | out of scope |
| fake standards/thresholds | unsafe and unscientific |
| future output as AI input | label leakage |
| GNN without baselines | weak evaluation |
| dashboard with fake hard-coded data | empty demo |
| claim real-fire accuracy | no real fire data |
| claim regulatory approval | invalid |

## EN — Forbidden

| Forbidden | Reason |
|---|---|
| full-building FDS for hundreds of cases | out of scope |
| fake standards/thresholds | unsafe and unscientific |
| future output as AI input | label leakage |
| GNN without baselines | weak evaluation |
| dashboard with fake hard-coded data | empty demo |
| claim real-fire accuracy | no real fire data |
| claim regulatory approval | invalid |

---

## VI — Definition of Done

| Module | Done when |
|---|---|
| IFC Parser | outputs node/edge tables with BIM IDs |
| Graph Builder | graph is visualized and checked |
| Scenario Generator | scenarios are reproducible |
| CFAST Runner | batch runs and logs errors |
| Post-processing | labels and time-series exist |
| IoT Simulator | clean/noisy/faulty streams exist |
| Dataset Builder | train/val/test splits exist |
| AI Model | baseline + model metrics exist |
| FDS Validation | selected cases compared at node-level |
| Dashboard | displays real pipeline outputs |
| Report | contains metrics, limitations, risks |

## EN — Definition of Done

| Module | Done when |
|---|---|
| IFC Parser | outputs node/edge tables with BIM IDs |
| Graph Builder | graph is visualized and checked |
| Scenario Generator | scenarios are reproducible |
| CFAST Runner | batch runs and logs errors |
| Post-processing | labels and time-series exist |
| IoT Simulator | clean/noisy/faulty streams exist |
| Dataset Builder | train/val/test splits exist |
| AI Model | baseline + model metrics exist |
| FDS Validation | selected cases compared at node-level |
| Dashboard | displays real pipeline outputs |
| Report | contains metrics, limitations, risks |
