# 06 — Virtual IoT and Dataset Plan / Kế hoạch IoT giả lập và dataset

## VI — Phương án cuối cùng

Dữ liệu IoT dùng trong đề tài là **Hybrid Virtual IoT Simulation**.

Không dùng trực tiếp toàn bộ output CFAST/FDS làm input AI. Output mô phỏng gốc dùng làm truth/label; input AI là dữ liệu cảm biến ảo đã được biến thành dữ liệu IoT không hoàn hảo.

## EN — Final approach

The project uses **Hybrid Virtual IoT Simulation**.

Do not directly use all CFAST/FDS outputs as AI inputs. Raw simulation outputs are used as truth/labels; AI inputs are virtual sensor streams transformed into imperfect IoT-like data.

---

## VI — Ba lớp dữ liệu

| Layer | Vai trò | AI input? |
|---|---|---|
| `physics_truth` | output mô phỏng gốc, label/ground truth | Không đưa trực tiếp toàn bộ |
| `virtual_sensor_clean` | cảm biến ảo sạch | Có, cho clean baseline |
| `iot_noisy_stream` | clean sensor + noise/delay/missing/fault | Có, input chính |

## EN — Three data layers

| Layer | Role | AI input? |
|---|---|---|
| `physics_truth` | raw simulation output, label/ground truth | not directly as full input |
| `virtual_sensor_clean` | clean virtual sensors | yes, for clean baseline |
| `iot_noisy_stream` | clean sensors + noise/delay/missing/fault | yes, main input |

---

## VI — Sensor P0/P1/P2

| Sensor/System | Variable | Priority |
|---|---|---|
| Smoke detector | `smoke_sensor(t)` | P0 |
| Temperature sensor | `temp_sensor(t)` | P0 |
| Door sensor | `door_sensor(t)` | P0/P1 |
| Alarm state | `alarm_state(t)` | P0 |
| CO sensor | `co_sensor(t)` | P1 |
| Sprinkler state | `sprinkler_state(t)` | P1 |
| Exhaust state | `exhaust_state(t)` | P1 |
| Pressurization state | `pressurization_state(t)` | P1 |
| Humidity sensor | `rh_sensor(t)` | P2 |
| HVAC/damper | `hvac_state(t)`, `damper_state(t)` | P2 |

## EN — P0/P1/P2 sensors

| Sensor/System | Variable | Priority |
|---|---|---|
| Smoke detector | `smoke_sensor(t)` | P0 |
| Temperature sensor | `temp_sensor(t)` | P0 |
| Door sensor | `door_sensor(t)` | P0/P1 |
| Alarm state | `alarm_state(t)` | P0 |
| CO sensor | `co_sensor(t)` | P1 |
| Sprinkler state | `sprinkler_state(t)` | P1 |
| Exhaust state | `exhaust_state(t)` | P1 |
| Pressurization state | `pressurization_state(t)` | P1 |
| Humidity sensor | `rh_sensor(t)` | P2 |
| HVAC/damper | `hvac_state(t)`, `damper_state(t)` | P2 |

---

## VI — IoT presets

| Preset | Meaning |
|---|---|
| `clean` | no noise/delay/missing |
| `low_noise` | light noise and small delay |
| `medium_noise` | moderate noise, delay, missing data |
| `faulty` | stuck/offline/drift/false alarm |
| `no_iot` | ablation setting |

## EN — IoT presets

| Preset | Meaning |
|---|---|
| `clean` | no noise/delay/missing |
| `low_noise` | light noise and small delay |
| `medium_noise` | moderate noise, delay, missing data |
| `faulty` | stuck/offline/drift/false alarm |
| `no_iot` | ablation setting |

---

## VI — Quy tắc chống label leakage

At time `t`, AI can only use data from `[t-k, t]`.

Forbidden:

- future CFAST/FDS outputs;
- `smoke_label[t+h]` as input;
- `arrival_time` as input;
- `unsafe_time` as input;
- `smoke_path` as input;
- same base scenario with different noise seeds in both train and test.

## EN — Label leakage prevention

At time `t`, AI can only use data from `[t-k, t]`.

Forbidden:

- future CFAST/FDS outputs;
- `smoke_label[t+h]` as input;
- `arrival_time` as input;
- `unsafe_time` as input;
- `smoke_path` as input;
- same base scenario with different noise seeds in both train and test.

---

## VI — Dataset output

| File | Content |
|---|---|
| `scenario_catalog.parquet` | scenario metadata |
| `building_graph.json` | graph topology |
| `node_features.parquet` | static node features |
| `edge_features.parquet` | static edge features |
| `physics_truth.parquet` | raw/processed simulation truth |
| `virtual_sensor_clean.parquet` | clean virtual sensor data |
| `iot_noisy_stream.parquet` | noisy/faulty IoT stream |
| `labels.parquet` | labels |
| `splits/train.txt` | train scenario IDs |
| `splits/val.txt` | validation scenario IDs |
| `splits/test.txt` | test scenario IDs |
| `pyg/*.pt` | PyTorch Geometric data objects |

## EN — Dataset output

| File | Content |
|---|---|
| `scenario_catalog.parquet` | scenario metadata |
| `building_graph.json` | graph topology |
| `node_features.parquet` | static node features |
| `edge_features.parquet` | static edge features |
| `physics_truth.parquet` | raw/processed simulation truth |
| `virtual_sensor_clean.parquet` | clean virtual sensor data |
| `iot_noisy_stream.parquet` | noisy/faulty IoT stream |
| `labels.parquet` | labels |
| `splits/train.txt` | train scenario IDs |
| `splits/val.txt` | validation scenario IDs |
| `splits/test.txt` | test scenario IDs |
| `pyg/*.pt` | PyTorch Geometric data objects |
