# 12 — Acceptance Checklist / Checklist nghiệm thu

## VI — P0 acceptance checklist

| Item | Pass condition |
|---|---|
| Scope | scope is locked and limitations are explicit |
| IFC export | IFC file exists and is inspectable |
| IFC parsing | rooms/doors/windows/floors/stairs extracted |
| Graph | graph is visualized and manually checked |
| Mapping | BIM GlobalId ↔ node/edge ID mapping exists |
| Low-rise layout | debug layout runs |
| CFAST | at least one batch set runs successfully |
| Post-processing | node time-series are created |
| Labels | `smoke_label` and `arrival_time` exist |
| IoT | clean/noisy/faulty streams exist |
| Dataset | scenario-level train/val/test splits exist |
| Baseline | rule-based and ML/MLP baseline metrics exist |
| GNN | graph/time model runs |
| Evaluation | metrics tables exist |
| FDS P0 | at least 3 validation cases if hardware allows |
| Dashboard | replay + graph + AI inference work |
| Report | results, limitations, risks, future work included |

## EN — P0 acceptance checklist

| Item | Pass condition |
|---|---|
| Scope | scope is locked and limitations are explicit |
| IFC export | IFC file exists and is inspectable |
| IFC parsing | rooms/doors/windows/floors/stairs extracted |
| Graph | graph is visualized and manually checked |
| Mapping | BIM GlobalId ↔ node/edge ID mapping exists |
| Low-rise layout | debug layout runs |
| CFAST | at least one batch set runs successfully |
| Post-processing | node time-series are created |
| Labels | `smoke_label` and `arrival_time` exist |
| IoT | clean/noisy/faulty streams exist |
| Dataset | scenario-level train/val/test splits exist |
| Baseline | rule-based and ML/MLP baseline metrics exist |
| GNN | graph/time model runs |
| Evaluation | metrics tables exist |
| FDS P0 | at least 3 validation cases if hardware allows |
| Dashboard | replay + graph + AI inference work |
| Report | results, limitations, risks, future work included |

---

## VI — Quality gates

| Gate | Must be true |
|---|---|
| Gate 1 | Graph is correct enough before CFAST automation |
| Gate 2 | CFAST parser works before dataset expansion |
| Gate 3 | Labels are created before AI training |
| Gate 4 | Baselines exist before GNN |
| Gate 5 | IoT leakage checks pass before model evaluation |
| Gate 6 | Dashboard uses real pipeline outputs |
| Gate 7 | Report states limitations and assumptions |

## EN — Quality gates

| Gate | Must be true |
|---|---|
| Gate 1 | Graph is correct enough before CFAST automation |
| Gate 2 | CFAST parser works before dataset expansion |
| Gate 3 | Labels are created before AI training |
| Gate 4 | Baselines exist before GNN |
| Gate 5 | IoT leakage checks pass before model evaluation |
| Gate 6 | Dashboard uses real pipeline outputs |
| Gate 7 | Report states limitations and assumptions |
