# 03 — BIM/IFC-to-Graph Plan / Kế hoạch BIM/IFC-to-Graph

## VI — Quyết định kỹ thuật

Không cố đọc trực tiếp file `.rvt` bằng Python thường. Đường triển khai ổn định:

```text
Revit
→ Export IFC
→ Parse IFC with IfcOpenShell
→ Build graph with NetworkX
→ Save graph + BIM mapping
```

## EN — Technical decision

Do not try to read `.rvt` directly with normal Python tools. Stable implementation path:

```text
Revit
→ Export IFC
→ Parse IFC with IfcOpenShell
→ Build graph with NetworkX
→ Save graph + BIM mapping
```

---

## VI — Việc cần làm trong Revit

1. Kiểm tra số tầng và tầng hầm.
2. Kiểm tra `Room`/`Space` đã được đặt chưa.
3. Nếu thiếu Room cho hành lang/cầu thang/sảnh, phải bổ sung hoặc tạo node thủ công sau.
4. Export IFC:
   - ưu tiên IFC4;
   - nếu lỗi parser, dùng IFC2x3;
   - bật export rooms/spaces;
   - bật space boundaries nếu có;
   - include doors, windows, walls, slabs, stairs, building storeys.

## EN — Tasks in Revit

1. Check floor count and basement levels.
2. Check whether `Room`/`Space` objects exist.
3. If corridors/stairs/lobbies are missing as rooms/spaces, add them or create nodes manually later.
4. Export IFC:
   - prefer IFC4;
   - if parser errors occur, use IFC2x3;
   - enable room/space export;
   - enable space boundaries if available;
   - include doors, windows, walls, slabs, stairs, building storeys.

---

## VI — IFC entities cần lấy

| Dữ liệu cần lấy | IFC entity | Graph usage |
|---|---|---|
| Tầng/cao độ | `IfcBuildingStorey` | floor/elevation |
| Phòng/khu vực | `IfcSpace` | node |
| Diện tích/thể tích | `Qto_SpaceBaseQuantities` | node feature |
| Quan hệ kề | `IfcRelSpaceBoundary` | adjacency |
| Cửa | `IfcDoor` | door edge |
| Cửa sổ | `IfcWindow` | window/outside edge |
| Cầu thang | `IfcStair` | stair node/vertical edge |
| Tường/sàn/trần | `IfcWall`, `IfcSlab` | material/compartment |
| ID gốc | `GlobalId` | BIM-to-graph traceability |

## EN — IFC entities to extract

| Required data | IFC entity | Graph usage |
|---|---|---|
| Floors/elevations | `IfcBuildingStorey` | floor/elevation |
| Rooms/zones | `IfcSpace` | node |
| Area/volume | `Qto_SpaceBaseQuantities` | node feature |
| Adjacency | `IfcRelSpaceBoundary` | adjacency |
| Doors | `IfcDoor` | door edge |
| Windows | `IfcWindow` | window/outside edge |
| Stairs | `IfcStair` | stair node/vertical edge |
| Walls/slabs/ceilings | `IfcWall`, `IfcSlab` | material/compartment |
| Original ID | `GlobalId` | BIM-to-graph traceability |

---

## VI — Graph design

### Node types

- `room`
- `corridor`
- `stair`
- `shaft`
- `lobby`
- `outside`

### Edge types

- `door`
- `window`
- `opening`
- `corridor_link`
- `stair_vertical`
- `shaft_vertical`
- `outside_connection`

## EN — Graph design

### Node types

- `room`
- `corridor`
- `stair`
- `shaft`
- `lobby`
- `outside`

### Edge types

- `door`
- `window`
- `opening`
- `corridor_link`
- `stair_vertical`
- `shaft_vertical`
- `outside_connection`

---

## VI — Output bắt buộc

| File | Nội dung |
|---|---|
| `node_map.csv` | `node_id`, IFC GlobalId, name, floor, node_type |
| `edge_map.csv` | `edge_id`, source, target, edge_type, IFC GlobalId |
| `building_graph.json` | topology + static features |
| `building_graph.graphml` | visualization/debug |
| `graph_check_report.md` | lỗi topology và chỉnh sửa thủ công |

## EN — Required outputs

| File | Content |
|---|---|
| `node_map.csv` | `node_id`, IFC GlobalId, name, floor, node_type |
| `edge_map.csv` | `edge_id`, source, target, edge_type, IFC GlobalId |
| `building_graph.json` | topology + static features |
| `building_graph.graphml` | visualization/debug |
| `graph_check_report.md` | topology errors and manual fixes |

---

## VI — Fallback nếu IFC lỗi

Nếu IFC không đủ sạch:

1. Vẫn giữ IFC làm nguồn chính.
2. Dựng graph bán thủ công từ:
   - mặt bằng;
   - room list;
   - door/window location;
   - floor plan.
3. Ghi rõ mọi chỉnh sửa trong `graph_check_report.md`.
4. Không giấu việc graph đã được sửa tay.

## EN — Fallback if IFC is messy

If IFC is not clean enough:

1. Still keep IFC as the primary source.
2. Build a semi-manual graph from:
   - floor plans;
   - room list;
   - door/window locations;
   - floor plan geometry.
3. Document all corrections in `graph_check_report.md`.
4. Do not hide manual graph corrections.
