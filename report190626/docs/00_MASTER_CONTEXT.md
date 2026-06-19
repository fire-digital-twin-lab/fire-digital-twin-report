# 00 — Master Context / Ngữ cảnh tổng thể

## VI — Đề tài

**Số hóa lan truyền khói trong tòa nhà dựa trên BIM/IFC, CFAST/FDS, IoT giả lập, điều kiện biên và học sâu dạng graph-time-series.**

Đây là đề tài nghiên cứu khoa học sinh viên. Mục tiêu là xây dựng một prototype end-to-end để dự đoán lan truyền khói ở cấp phòng/khu vực trong tòa nhà cao tầng/chung cư.

## EN — Project

**Digitalizing smoke spread in buildings using BIM/IFC, CFAST/FDS, virtual IoT, boundary conditions, and graph-time-series deep learning.**

This is a student research project. The goal is to build an end-to-end prototype for room/zone-level smoke-spread prediction in a high-rise/residential building.

---

## VI — Bài toán

Cho một mô hình BIM/Revit/IFC của tòa nhà, xây dựng hệ thống dự đoán:

- node nào có khói theo thời gian;
- thời điểm khói đến từng node;
- node nào có nguy cơ mất an toàn;
- đường lan truyền khói;
- trạng thái cảm biến và hệ thống PCCC dưới dạng giả lập.

Node có thể là:

- phòng;
- hành lang;
- cầu thang;
- shaft/trục kỹ thuật;
- sảnh thang;
- outside node liên quan đến cửa sổ/lỗ mở.

## EN — Problem

Given a BIM/Revit/IFC building model, build a system that predicts:

- which node contains smoke over time;
- smoke arrival time at each node;
- which node may become unsafe;
- the predicted smoke-spread path;
- simulated sensor and fire-protection system states.

A node can be:

- room;
- corridor;
- stair;
- shaft;
- elevator/stair lobby;
- outside node associated with windows/openings.

---

## VI — Luận điểm nghiên cứu

Tính mới không nằm ở việc phát minh ra BIM, CFAST, FDS, IoT hay GNN. Tính mới nằm ở pipeline tích hợp:

```text
BIM/IFC
→ Building Graph
→ Scenario Generator
→ CFAST/FDS
→ Virtual IoT
→ Graph-Time-Series Dataset
→ AI Surrogate Model
→ Dashboard
```

## EN — Research claim

The novelty is not in inventing BIM, CFAST, FDS, IoT, or GNN. The novelty lies in the integrated pipeline:

```text
BIM/IFC
→ Building Graph
→ Scenario Generator
→ CFAST/FDS
→ Virtual IoT
→ Graph-Time-Series Dataset
→ AI Surrogate Model
→ Dashboard
```

---

## VI — Sản phẩm cuối cùng

| Sản phẩm | Bắt buộc |
|---|---|
| Báo cáo nghiên cứu | Có |
| Module BIM/IFC-to-Graph | Có |
| Building graph của tòa thực tế hoặc cụm tầng | Có |
| Layout thấp tầng debug | Có |
| Bộ kịch bản cháy P0/P1 | Có |
| Dataset từ CFAST | Có |
| FDS validation P0/P1 | Có nếu đủ phần cứng, tối thiểu P0 |
| Virtual IoT dataset | Có |
| AI dataset graph + time-series | Có |
| Baseline models | Có |
| Temporal GNN/BAT-GNN prototype | Có |
| Dashboard prototype | Có |
| Evaluation report | Có |

## EN — Final deliverables

| Deliverable | Required |
|---|---|
| Research report | Yes |
| BIM/IFC-to-Graph module | Yes |
| Building graph of real building or floor cluster | Yes |
| Low-rise debug layout | Yes |
| P0/P1 fire scenarios | Yes |
| CFAST dataset | Yes |
| P0/P1 FDS validation | Yes if hardware allows; at least P0 |
| Virtual IoT dataset | Yes |
| Graph + time-series AI dataset | Yes |
| Baseline models | Yes |
| Temporal GNN/BAT-GNN prototype | Yes |
| Dashboard prototype | Yes |
| Evaluation report | Yes |

---

## VI — Câu mô tả ngắn cho agent

> Xây dựng prototype nghiên cứu dự đoán lan truyền khói cấp phòng/khu vực trong tòa nhà cao tầng. CFAST sinh dataset chính, FDS kiểm chứng chọn lọc, IoT là cảm biến ảo 3 lớp, AI là surrogate model, dashboard chỉ để replay/inference/visualization.

## EN — Short instruction for agents

> Build a research prototype for room/zone-level smoke-spread prediction in high-rise buildings. CFAST generates the main dataset, FDS validates selected cases, IoT is a three-layer virtual sensor system, AI is a surrogate model, and the dashboard is only for replay/inference/visualization.
