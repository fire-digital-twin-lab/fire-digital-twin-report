# 07 — AI Model and Evaluation Plan / Kế hoạch mô hình AI và đánh giá

## VI — Vai trò AI

AI là **surrogate model** để dự đoán nhanh từ dữ liệu graph + time-series. AI không thay thế CFAST/FDS và không tạo kết luận pháp lý.

## EN — AI role

AI is a **surrogate model** for fast prediction from graph + time-series data. It does not replace CFAST/FDS and does not produce legal conclusions.

---

## VI — Lộ trình mô hình

| Level | Model | Purpose |
|---|---|---|
| 0 | Rule-based graph spread | minimum baseline |
| 1 | Logistic Regression / Random Forest / XGBoost | tabular baseline |
| 2 | MLP | feature baseline without graph |
| 3 | LSTM/GRU/TCN | time-series baseline |
| 4 | GCN/GraphSAGE/GAT | graph baseline |
| 5 | Temporal GNN | graph + time |
| 6 | Boundary-aware Temporal GNN | main model |

## EN — Model roadmap

| Level | Model | Purpose |
|---|---|---|
| 0 | Rule-based graph spread | minimum baseline |
| 1 | Logistic Regression / Random Forest / XGBoost | tabular baseline |
| 2 | MLP | feature baseline without graph |
| 3 | LSTM/GRU/TCN | time-series baseline |
| 4 | GCN/GraphSAGE/GAT | graph baseline |
| 5 | Temporal GNN | graph + time |
| 6 | Boundary-aware Temporal GNN | main model |

---

## VI — Main model

```text
Input:
  Graph G(V,E)
  Node static/dynamic features
  Edge static/dynamic features
  Global boundary features
  Fire features
  System state features

Encoders:
  Graph Encoder
  Temporal Encoder
  Boundary Encoder
  Fire Encoder
  System Encoder

Fusion:
  concat or attention

Decoders:
  smoke_label
  hazard_label
  arrival_time
  unsafe_time
  next_affected_node
```

## EN — Main model

```text
Input:
  Graph G(V,E)
  Node static/dynamic features
  Edge static/dynamic features
  Global boundary features
  Fire features
  System state features

Encoders:
  Graph Encoder
  Temporal Encoder
  Boundary Encoder
  Fire Encoder
  System Encoder

Fusion:
  concat or attention

Decoders:
  smoke_label
  hazard_label
  arrival_time
  unsafe_time
  next_affected_node
```

---

## VI — Loss

| Output | Loss |
|---|---|
| `smoke_label` | BCE or Focal Loss |
| `hazard_label` | BCE or Focal Loss |
| `arrival_time` | MAE/MSE/Huber |
| `unsafe_time` | MAE/MSE/Huber |
| `next_affected_node` | Cross Entropy |
| multi-task | weighted sum |

## EN — Loss

| Output | Loss |
|---|---|
| `smoke_label` | BCE or Focal Loss |
| `hazard_label` | BCE or Focal Loss |
| `arrival_time` | MAE/MSE/Huber |
| `unsafe_time` | MAE/MSE/Huber |
| `next_affected_node` | Cross Entropy |
| multi-task | weighted sum |

---

## VI — Metrics

| Task | Metrics |
|---|---|
| Smoke classification | F1, Recall, Precision, AUC |
| Hazard classification | Recall, F1, AUC |
| Arrival time | MAE, RMSE |
| Unsafe time | MAE, RMSE |
| Path | path accuracy, next-node accuracy |
| Calibration | Brier score, calibration curve if available |
| Speed | inference time |
| Robustness | metric drop under noisy/faulty IoT |

Important: In fire-safety tasks, **Recall is more important than Accuracy** because missing hazardous zones is worse than over-predicting risk.

## EN — Metrics

| Task | Metrics |
|---|---|
| Smoke classification | F1, Recall, Precision, AUC |
| Hazard classification | Recall, F1, AUC |
| Arrival time | MAE, RMSE |
| Unsafe time | MAE, RMSE |
| Path | path accuracy, next-node accuracy |
| Calibration | Brier score, calibration curve if available |
| Speed | inference time |
| Robustness | metric drop under noisy/faulty IoT |

Important: In fire-safety tasks, **Recall is more important than Accuracy** because missing hazardous zones is worse than over-predicting risk.

---

## VI — Dataset splits

| Split | Purpose |
|---|---|
| scenario split | basic evaluation |
| hold-out fire node | new ignition location |
| hold-out fire floor | new fire floor |
| hold-out layout | new layout/building |
| noise robustness split | degraded IoT |
| FDS validation set | compare with detailed CFD |

## EN — Dataset splits

| Split | Purpose |
|---|---|
| scenario split | basic evaluation |
| hold-out fire node | new ignition location |
| hold-out fire floor | new fire floor |
| hold-out layout | new layout/building |
| noise robustness split | degraded IoT |
| FDS validation set | compare with detailed CFD |

---

## VI — Ablation study

| Experiment | Meaning |
|---|---|
| Graph only | topology contribution |
| Graph + Fire | fire source contribution |
| Graph + IoT | sensor contribution |
| Graph + Boundary | boundary condition contribution |
| Graph + System | sprinkler/exhaust/pressurization contribution |
| Full model | all features |
| Full without IoT | IoT usefulness |
| Full without Boundary | boundary usefulness |

## EN — Ablation study

| Experiment | Meaning |
|---|---|
| Graph only | topology contribution |
| Graph + Fire | fire source contribution |
| Graph + IoT | sensor contribution |
| Graph + Boundary | boundary condition contribution |
| Graph + System | sprinkler/exhaust/pressurization contribution |
| Full model | all features |
| Full without IoT | IoT usefulness |
| Full without Boundary | boundary usefulness |
