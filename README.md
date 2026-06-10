[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112728&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** olivia.ngocanh208@gmail.com
**Name:** Nguyen Ngoc Anh

---

## Mo ta

Bai lab nay xay dung mot ETL Pipeline hoan chinh de xu ly du lieu san pham tu file JSON. Pipeline thuc hien 4 buoc: Extract (doc du lieu JSON), Validate (loai bo records co gia <= 0 hoac category trong), Transform (tinh gia giam 10% va chuan hoa category thanh Title Case), va Load (luu ket qua ra CSV). Ngoai ra, thi nghiem Stress Test so sanh ket qua cua Agent khi su dung Clean Data vs Garbage Data de minh hoa tam quan trong cua chat luong du lieu.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```
Pipeline se doc `raw_data.json`, validate, transform va luu ket qua ra `processed_data.csv`.

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Chay pipeline de tao clean data
python solution.py

# Buoc 2: Tao garbage data
python generate_garbage.py

# Buoc 3: Chay agent simulation voi ca hai loai du lieu
python agent_simulation.py
```

### Chay Tests
```bash
pytest tests/
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script (extract, validate, transform, load)
├── raw_data.json            # Du lieu dau vao (5 records, 2 bi loai)
├── processed_data.csv       # Output cua pipeline (3 records hop le)
├── garbage_data.csv         # Du lieu "rac" cho stress test
├── generate_garbage.py      # Script tao garbage data
├── agent_simulation.py      # Agent simulation de test data quality
├── experiment_report.md     # Bao cao thi nghiem stress test
└── README.md                # File nay
```

---

## Ket qua

- **Tong so records doc vao:** 5
- **Records hop le (giu lai):** 3 (Laptop, Chair, Monitor)
- **Records bi loai:** 2 (Mystery Box: price=-10, Phone: category rong)
- **Ket qua transform:** Them cot `discounted_price` (giam 10%) va `processed_at` (timestamp)
- **Stress Test:** Clean Data → Agent tra loi dung (Laptop $1200); Garbage Data → Agent bi danh lua boi outlier (Nuclear Reactor $999999)
