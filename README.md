# Mini Financial Audit Tool

ระบบเครื่องมือตรวจสอบข้อมูลการเงินย่อย (Audit Suite & Web Dashboard) ที่เน้นความมั่นคงปลอดภัยของข้อมูลตามมาตรฐาน Read-Only และ Zero PII Leakage

## คุณสมบัติหลัก (Key Features)
- **Read-Only SQLite Database Connection**: เชื่อมต่อฐานข้อมูลผ่าน URI `file:...mode=ro` ป้องกันการแก้ไขหรือลบข้อมูลต้นทาง 100%
- **Unified Web Dashboard & CLI Suite**:
  - Main Dashboard (`/`): ภาพรวมสถานะระบบและ Aggregate KPI Metrics
  - Data Quality (`/data-quality`): ตรวจสอบคุณภาพข้อมูล 4 มิติ
  - Fast In/Out Results (`/fast-in-out-results`): ตรวจจับธุรกรรมเงินเข้า-ออกเร็ว พร้อม Masking เลขบัญชี
  - Safe Data Verification (`/safe-data-check`): หน้าตรวจสอบ Safe Data พร้อมระบบ Human Approval Gate ก่อน Export
- **Dynamic Dataset Configuration**: รองรับการเปลี่ยนตำแหน่ง Dataset ผ่าน `AUDIT_DB_PATH` โดยไม่ต้องแก้ Core Logic
- **Strict Privacy & Security**: แสดงผลเฉพาะ Aggregate Statistics และ Allowlist Fields ปราศจาก Raw PII Leakage

## วิธีการใช้งาน (How to Run)

### 1. เรียกใช้งานผ่าน Web Dashboard (FastAPI / Uvicorn)
```bash
python -m uvicorn app.main:app --reload
```
เข้าใช้งานผ่านเบราว์เซอร์ที่ `http://127.0.0.1:8000`

### 2. เรียกใช้งานผ่าน CLI Script
```bash
# รันชุดตรวจสอบ Audit Suite หลัก
python audit_suite.py

# รันชุดตรวจจับ Cashflow Drain
python cashflow_drain.py --large_in_min 500000 --outflow_ratio_min 0.80 --window_days 3
```

## การเปลี่ยน Dataset Path (Changing Dataset)
คุณสามารถเปลี่ยนตำแหน่งฐานข้อมูลได้โดยตรงผ่าน Environment Variable `AUDIT_DB_PATH` ทั้งใน CLI และ Web App:
```bash
# บน Linux/macOS
export AUDIT_DB_PATH="file:data/custom_dataset.sqlite3?mode=ro"

# บน Windows PowerShell
$env:AUDIT_DB_PATH="file:data/custom_dataset.sqlite3?mode=ro"
```
*(ระบบบังคับเติม `?mode=ro` ให้อัตโนมัติหากระบุเป็น Relative Path ทั่วไป เพื่อรักษาความปลอดภัยระดับ Driver)*
