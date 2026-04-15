[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574028&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.trangdtt@vinuni.edu.vn
**Name:** Do Thi Thuy Trang

---

## Mo ta

Xây dựng 1 luồng ETL cơ bản để xử lý dữ liệu và ảnh hưởng của chất lượng dữ liệu đến câu trả lời của AI Agent.

Cụ thể những gì đã làm: 
- Đọc dữ liệu từ file JSON (`extract`).
- Kiểm tra và loại bản ghi không hợp lệ (`validate`).
- Chuẩn hóa dữ liệu (`transform`).
- Lưu dữ liệu đã được xử lý ra CSV (`load`).
- Chạy mô phỏng Agent với dữ liệu đã được xử lý và dữ liệu chưa xử lý để quan sát sự khác biệt.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Mo ta cach ban chay thi nghiem Clean vs Garbage data
python .\generate_garbage.py    
python .\agent_simulation.py   
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

**Kết quả ETL Pipeline:**
- **Tổng số Records đầu vào:** 5 (từ raw_data.json)
- **Records hợp lệ:** 3 ✓
- **Records không hợp lệ (bị loại):** 2 ✗
  - Record ID=3 (Mystery Box): Nagative Price (-$10) - validation thất bại
  - Record ID=4 (Phone): Empty Category - validation thất bại

**Output Data (processed_data.csv):**
```
1. Laptop - $1,200 (Electronics) → Discounted: $1,080
2. Chair - $45 (Furniture) → Discounted: $40.50
3. Monitor - $300 (Electronics) → Discounted: $270
```

**Kết quả Agent Simulation:**
- Clean Data Test: **THÀNH CÔNG** ✓ - Agent: Based on my data, the best choice is Laptop at $1200.
- Garbage Data Test: **THẤT BẠI** ✗ - Agent Error: I'm choking on the data! (reduction operation 'argmax' not allowed for this dtype)

**Phát hiện chính:** Chất lượng dữ liệu có ảnh hưởng khổng lồ đến độ tin cậy của AI agent. Dữ liệu tệ = AI tệ!
