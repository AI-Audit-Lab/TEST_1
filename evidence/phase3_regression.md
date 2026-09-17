# Phase 3 Regression Test Report

## 1. Overview
- **Date**: 2026-09-17
- **Target**: Phase 3 Gap Fix (Web App `AUDIT_DB_PATH` alignment and read-only URI enforcement)
- **Database Status**: `file:data/training_data.sqlite3?mode=ro` (Strict Read-Only)

---

## 2. Standalone Regression Test Results

### 2.1 Data Quality Check Suite (`test_data_quality.py`)
- **Status**: SUCCESS (100% Passed)
- **Total Transactions Checked**: 608
- **Unmatched Account IDs**: 1
- **Duplicate Source Ref Groups**: 1 (2 rows)
- **Invalid Tx Codes**: 1
- **Overall Pass Rate**: 99.34%
- **Expected Result Status**: UNKNOWN

### 2.2 Fast In/Out 3D Test Suite (`test_fast_in_out.py`)
- **Status**: SUCCESS (7/7 Test Cases Passed)
  - `[TC-01]` Default values (500000, 0.80, 3): PASSED
  - `[TC-02]` Boundary values (500000, 1.0, 1): PASSED
  - `[TC-03]` Inclusive boundary checks: PASSED
  - `[TC-04]` Pre-query validation - invalid large_in_min: PASSED
  - `[TC-05]` Pre-query validation - invalid outflow_ratio_min: PASSED
  - `[TC-06]` Pre-query validation - invalid window_days: PASSED
  - `[TC-07]` In-memory edge cases (boundary, cancelled exclusion, time window): PASSED

### 2.3 Safe Export & Approval Gate Suite (`test_safe_export_approval.py`)
- **Status**: SUCCESS (5/5 Test Cases Passed)
  - `[TC-01]` Default unapproved state blocked (HTTP 403): PASSED
  - `[TC-02]` Explicit rejection flow & logging: PASSED
  - `[TC-03]` Approved export (CSV, Excel, PDF): PASSED
  - `[TC-04]` Zero PII, zero secrets, zero token map leakage: PASSED
  - `[TC-05]` Sanitized audit log verification: PASSED

---

## 3. Web App Health & Live Service
- **Uvicorn Daemon**: Running on `http://127.0.0.1:8000`
- **Health Check Endpoint (`/api/v1/health`)**: Status `online`, Database mode `read-only`
- **Result**: ALL REGRESSION CHECKS PASSED (Ready for Baseline Save)
