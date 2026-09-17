# Changelog

## [Unreleased] - 2026-09-17

### Added / Changed (Approved Gap Fixes - Phase 3)
- **Web App Dataset Path Alignment**: ปรับปรุง [`app/config.py`](file:///d:/AI_AUDIT_LAB/app/config.py) ให้รองรับ Environment Variable `AUDIT_DB_PATH` เป็นลำดับแรก เพื่อให้สอดคล้องกับ `README.md`, `audit_suite.py` และ `cashflow_drain.py` รองรับการทดสอบ Refresh Dataset Test (ข้อ 3.7)
- **Automatic Read-Only Mode Enforcement**: เพิ่มการตรวจสอบและเติม `?mode=ro` อัตโนมัติใน `app/config.py` เมื่อรับ Dataset Path แบบข้อความธรรมดา
- **Documentation Update**: ปรับปรุง [`README.md`](file:///d:/AI_AUDIT_LAB/README.md) ระบุภาพรวมของ Web App ทุกหน้าจอ, ขั้นตอนการรัน และการสลับ Dataset ผ่าน `AUDIT_DB_PATH`

### Regression Tests Passed
- `pytest test_data_quality.py` — ผ่าน 100%
- `pytest test_fast_in_out.py` — ผ่าน 100%
- `pytest test_safe_export_approval.py` — ผ่าน 100%
- Web App Uvicorn Dev Server (`app.main:app`) เชื่อมต่อฐานข้อมูลสำเร็จในโหมด Read-Only

### Constraints & Security Guarantees
- ไม่มีการเปิด Raw Data หรือ PII
- ไม่มีการเพิ่ม External Package หรือ Dependencies ใหม่ (ใช้ standard library `os`)
- คง Parameterized Query, Validation, Data Treatment Matrix และ Audit Logic เดิมทั้งหมด
- ข้อจำกัด: Dataset ใหม่ต้องมีโครงสร้างตารางและคอลัมน์สอดคล้องกับ SQLite schema ของระบบ
