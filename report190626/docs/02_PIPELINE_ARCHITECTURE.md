# 02 — Pipeline Architecture / Kiến trúc pipeline

## VI — Pipeline chính

```text
Revit/BIM
   ↓
Export IFC
   ↓
IFC Parser
   ↓
Building Graph
   ↓
Scenario Generator
   ↓
CFAST Batch Simulation
   ↓
Post-processing
   ↓
Virtual IoT Simulation
   ↓
Graph-Time-Series Dataset
   ↓
AI Baselines
   ↓
Temporal GNN / Boundary-aware Temporal GNN
   ↓
Inference API
   ↓
Dashboard Prototype
```

## EN — Main pipeline

```text
Revit/BIM
   ↓
Export IFC
   ↓
IFC Parser
   ↓
Building Graph
   ↓
Scenario Generator
   ↓
CFAST Batch Simulation
   ↓
Post-processing
   ↓
Virtual IoT Simulation
   ↓
Graph-Time-Series Dataset
   ↓
AI Baselines
   ↓
Temporal GNN / Boundary-aware Temporal GNN
   ↓
Inference API
   ↓
Dashboard Prototype
```

---

## VI — Nhánh FDS validation

```text
Selected Representative Scenarios
   ↓
Simplified FDS Geometry
   ↓
FDS Simulation
   ↓
Smokeview + Device/Slice Output
   ↓
Node-level Aggregation
   ↓
Comparison:
   CFAST vs FDS vs AI
```

## EN — FDS validation branch

```text
Selected Representative Scenarios
   ↓
Simplified FDS Geometry
   ↓
FDS Simulation
   ↓
Smokeview + Device/Slice Output
   ↓
Node-level Aggregation
   ↓
Comparison:
   CFAST vs FDS vs AI
```

---

## VI — Data flow nguyên tắc

| Stage | Input | Output |
|---|---|---|
| IFC Parser | `.ifc` | raw BIM tables |
| Graph Builder | BIM tables | `building_graph.json`, `node_map.csv`, `edge_map.csv` |
| Scenario Generator | graph + factor configs | scenario configs |
| CFAST Runner | scenario configs | raw CFAST outputs |
| Post-processing | raw outputs | node time-series + labels |
| IoT Simulator | node time-series | clean/noisy/faulty sensor streams |
| Dataset Builder | graph + sensors + labels | model-ready dataset |
| AI Trainer | dataset | model + metrics |
| Dashboard API | graph + sensors + predictions | REST/WS endpoints |

## EN — Data flow principle

| Stage | Input | Output |
|---|---|---|
| IFC Parser | `.ifc` | raw BIM tables |
| Graph Builder | BIM tables | `building_graph.json`, `node_map.csv`, `edge_map.csv` |
| Scenario Generator | graph + factor configs | scenario configs |
| CFAST Runner | scenario configs | raw CFAST outputs |
| Post-processing | raw outputs | node time-series + labels |
| IoT Simulator | node time-series | clean/noisy/faulty sensor streams |
| Dataset Builder | graph + sensors + labels | model-ready dataset |
| AI Trainer | dataset | model + metrics |
| Dashboard API | graph + sensors + predictions | REST/WS endpoints |

---

## VI — Folder structure

```text
project_root/
  docs/
  bim/
    raw_revit/
    raw_ifc/
    cleaned_ifc/
  graph/
    node_map.csv
    edge_map.csv
    building_graph.json
    building_graph.graphml
    graph_check_report.md
  scenarios/
    scenario_catalog.parquet
    configs/
    splits/
  simulations/
    cfast/
      raw/
      parsed/
      logs/
    fds/
      raw/
      aggregated/
      smokeview/
      logs/
  iot/
    clean/
    low_noise/
    medium_noise/
    faulty/
  dataset/
    processed/
    pyg/
  models/
    baselines/
    temporal_gnn/
    batgnn/
  dashboard/
    api/
    frontend/
  reports/
    figures/
    tables/
```

## EN — Folder structure

Use the structure above. Keep raw, parsed, processed, and model-ready data separate. Every scenario must have a scenario ID, config, metadata, and log files.
