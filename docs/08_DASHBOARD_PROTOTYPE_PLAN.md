# 08 — Dashboard Prototype Plan / Kế hoạch dashboard prototype

## VI — Vai trò

Dashboard chỉ phục vụ:

- replay scenario;
- AI inference;
- stream dữ liệu IoT giả lập;
- trực quan hóa graph, smoke, hazard, arrival time.

Dashboard không điều khiển hệ thống PCCC thật.

## EN — Role

The dashboard only supports:

- scenario replay;
- AI inference;
- virtual IoT stream;
- visualization of graph, smoke, hazard, arrival time.

It does not control real fire-protection systems.

---

## VI — Chức năng P0

| Feature | Description |
|---|---|
| Graph view | show nodes/edges |
| Floor filter | show selected floor/cluster |
| Sensor panel | virtual smoke/temp/door/alarm states |
| Smoke probability | AI prediction per node |
| Arrival time | arrival time per node |
| Replay scenario | play timeline |
| AI inference API | run model on selected scenario |
| CFAST vs AI | compare labels/predictions |

## EN — P0 features

| Feature | Description |
|---|---|
| Graph view | show nodes/edges |
| Floor filter | show selected floor/cluster |
| Sensor panel | virtual smoke/temp/door/alarm states |
| Smoke probability | AI prediction per node |
| Arrival time | arrival time per node |
| Replay scenario | play timeline |
| AI inference API | run model on selected scenario |
| CFAST vs AI | compare labels/predictions |

---

## VI — Chức năng P1

| Feature | Description |
|---|---|
| Hazard zone | show unsafe/proxy unsafe nodes |
| Predicted path | show predicted spread path |
| WebSocket/SSE stream | virtual real-time stream |
| CFAST/FDS/AI comparison | selected validation cases |
| System state | sprinkler/exhaust/pressurization |
| Robustness demo | clean vs noisy IoT |

## EN — P1 features

| Feature | Description |
|---|---|
| Hazard zone | show unsafe/proxy unsafe nodes |
| Predicted path | show predicted spread path |
| WebSocket/SSE stream | virtual real-time stream |
| CFAST/FDS/AI comparison | selected validation cases |
| System state | sprinkler/exhaust/pressurization |
| Robustness demo | clean vs noisy IoT |

---

## VI — Công nghệ đề xuất

| Layer | Technology |
|---|---|
| Backend | FastAPI |
| AI inference | PyTorch + FastAPI |
| Frontend | React + TypeScript |
| Graph visualization | Cytoscape.js or React Flow |
| Charts | ECharts or Recharts |
| Realtime | WebSocket or Server-Sent Events |
| Database | SQLite/PostgreSQL |
| Time-series storage | Parquet |
| Deployment | Docker Compose |

## EN — Recommended technology

| Layer | Technology |
|---|---|
| Backend | FastAPI |
| AI inference | PyTorch + FastAPI |
| Frontend | React + TypeScript |
| Graph visualization | Cytoscape.js or React Flow |
| Charts | ECharts or Recharts |
| Realtime | WebSocket or Server-Sent Events |
| Database | SQLite/PostgreSQL |
| Time-series storage | Parquet |
| Deployment | Docker Compose |

---

## VI — API gợi ý

| Endpoint | Purpose |
|---|---|
| `GET /scenarios` | list scenarios |
| `GET /scenarios/{id}` | scenario metadata |
| `GET /graph/{scenario_id}` | graph |
| `GET /timeseries/{scenario_id}` | sensor stream |
| `GET /labels/{scenario_id}` | labels |
| `POST /inference` | run AI inference |
| `GET /comparison/{scenario_id}` | CFAST/FDS/AI comparison |
| `WS /stream/{scenario_id}` | virtual IoT stream |

## EN — Suggested API

| Endpoint | Purpose |
|---|---|
| `GET /scenarios` | list scenarios |
| `GET /scenarios/{id}` | scenario metadata |
| `GET /graph/{scenario_id}` | graph |
| `GET /timeseries/{scenario_id}` | sensor stream |
| `GET /labels/{scenario_id}` | labels |
| `POST /inference` | run AI inference |
| `GET /comparison/{scenario_id}` | CFAST/FDS/AI comparison |
| `WS /stream/{scenario_id}` | virtual IoT stream |

---

## VI — Không được làm

- Không hard-code dữ liệu đẹp.
- Không hiển thị output không trace được về pipeline.
- Không gọi dashboard là hệ thống điều khiển PCCC.
- Không claim realtime CFD.
- Không claim an toàn pháp lý.

## EN — Do not

- Do not hard-code attractive fake data.
- Do not display outputs that cannot be traced back to the pipeline.
- Do not call the dashboard a fire-protection control system.
- Do not claim real-time CFD.
- Do not claim legal safety conclusions.
