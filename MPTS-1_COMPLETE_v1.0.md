# MPTS-1: Mr.Chuti Pre-Workshop Triage Standard
## Complete Standards Document v1.0

**Mr.Chuti อะไหล่ Mercedes-Benz มือสอง**
เบนซ์ W201 · W202 · W124 · W210 · W126 · W140

---

## 📋 Document Information

| Field | Value |
|-------|-------|
| Standard Suite | MPTS-1 |
| Document Version | 1.0 (Complete) |
| Owner | Mr.Chuti อะไหล่เบนซ์มือสอง |
| Compiled | 2026-05-07 |
| Language | Thai (primary) + English (technical) |
| Scope | W201 · W202 · W124 · W210 · W126 · W140 (เบนซินเท่านั้น) |
| Out of Scope | ดีเซล (OM601-OM606), W123, W203/W211/W220+ |

---

## 📑 Table of Contents

- [Executive Summary](#executive-summary)
- [§1 Vehicle Identity Standard](#1-vehicle-identity-standard)
- [§2 Symptom Intake Standard](#2-symptom-intake-standard)
- [§3 Safety & Stop-Drive Standard](#3-safety--stop-drive-standard)
- [§4 Evidence Capture Standard](#4-evidence-capture-standard)
- [§5 Workshop Handoff Standard](#5-workshop-handoff-standard)
- [§5-Sup Workshop Registration Standard](#5-sup-workshop-registration-standard)
- [§6 Outcome Verification Standard](#6-outcome-verification-standard)
- [Implementation Roadmap](#implementation-roadmap)
- [Appendices](#appendices)

---

# Executive Summary

## What is MPTS-1?

**MPTS-1** เป็น **operating standard** ของ Mr.Chuti อะไหล่เบนซ์มือสอง — ไม่ใช่แค่ "แบบฟอร์ม" แต่เป็นชุดมาตรฐานที่กำหนดวิธีการทำงานทั้งระบบ ตั้งแต่ลูกค้าแจ้งอาการ → จัดอะไหล่ → ส่งช่าง → ปิดเคส

## Why MPTS-1?

```
ปัญหาเดิม:
  ลูกค้า → "รถผมเสีย" → เดาอะไหล่ → ขายผิด → ลูกค้าหาย

หลังมี MPTS-1:
  ลูกค้า → ระบบวินิจฉัย → จัดอะไหล่ตรง → จับคู่ช่างใกล้บ้าน
        → ซ่อมหาย → feedback → ระบบฉลาดขึ้น
        → Mr.Chuti = "ที่นึงที่ไว้ใจได้" ของลูกค้า
```

## Architecture Overview

```
┌──────────────────────────────────────────────────┐
│                    LUKE-CHA                       │
│              (Customer-facing)                    │
└──────────────────────────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────┐
│  §1 Vehicle Identity   ← ระบุรถให้ตรง            │
│  §2 Symptom Intake     ← รวบอาการแบบโครงสร้าง    │
│  §3 Safety/Stop-Drive  ← คัดกรองอันตราย          │
│  §4 Evidence Capture   ← บังคับภาพประกอบ         │
└──────────────────────────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────┐
│              MR.CHUTI (Operations)                │
│  - จัดอะไหล่                                      │
│  - Match ช่างพาร์ทเนอร์ตามตำแหน่ง                 │
│  - ออกใบ Handoff (LINE+Sheet+PDF)                 │
└──────────────────────────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────┐
│  §5 Workshop Handoff       (ใบส่งงาน)             │
│  §5-Sup Workshop Reg       (ลงทะเบียน + verify)   │
└──────────────────────────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────┐
│           VERIFIED PARTNER WORKSHOPS              │
│           (ช่างพาร์ทเนอร์ verified)               │
└──────────────────────────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────┐
│  §6 Outcome Verification                          │
│  - 3-party feedback                               │
│  - 5 feedback loops → ระบบเรียนรู้เอง            │
└──────────────────────────────────────────────────┘
                        │
                        ▼
              ┌─────────────────────┐
              │  ระบบฉลาดขึ้นเรื่อยๆ  │
              └─────────────────────┘
                        │
                        └────► loop กลับ §1-§5
```

## Business Model

| ฝ่าย | รายได้จาก |
|------|-----------|
| **Mr.Chuti** | ขายอะไหล่ + referral fee 5-10% จากค่าแรงช่าง |
| **ช่างพาร์ทเนอร์** | ค่าแรง (หัก referral) |
| **ลูกค้า** | จ่าย 2 ฝ่ายแยกกัน — โปร่งใส |

## Trust Architecture

```
ลูกค้าเชื่อ Mr.Chuti (มาเพราะอะไหล่ดี)
        ↓
Mr.Chuti รับรอง (verified) ช่างพาร์ทเนอร์
        ↓
ลูกค้าเชื่อช่างพาร์ทเนอร์ (เพราะ Mr.Chuti รับรอง)
        ↓
Closed-loop Trust = Mr.Chuti brand แข็งแรง
```

---

# §1 Vehicle Identity Standard

## 🎯 วัตถุประสงค์

ระบุรถลูกค้าให้ตรง chassis + engine + ปี ก่อนแนะนำอะไหล่

## 🚨 หลักการ

| # | หลักการ | เหตุผล |
|---|--------|-------|
| P1 | ลูกค้าเป็นจุดเริ่ม ไม่ใช่ช่าง | ลูกค้าบอก "ตัว S" "ตัว E" "190E" ไม่บอก W126/W124/W201 |
| P2 | รุ่น + ปี = chassis code | ปีคือ disambiguator สำคัญที่สุด |
| P3 | ใช้ภาพช่วยเมื่อสงสัย | หน้ารถ/ท้ายรถเทียบกัน ลูกค้าชี้ได้เลย |
| P4 | Engine code มาทีหลัง | ระบบเดาให้จากรุ่น+ปี+ความจุ |
| P5 | AMG / 4MATIC เป็น variant | flag เพิ่มบน chassis เดิม |
| P6 | ขั้นต่ำที่ผ่าน = chassis + ปี + body style | ส่งต่อ §2 ได้ |

## 🚗 6 Chassis ที่ Mr.Chuti รับ

```
COMPACT/C-CLASS:
  W201 (1982-1993)  →  W202 (1993-2000)
       "190E"             "C-Class รุ่นแรก"

E-CLASS:
  W124 (1984-1996)  →  W210 (1995-2002)
       "ตัว E เก่า"       "ตัว E ตาเหยี่ยว"

S-CLASS:
  W126 (1979-1991)  →  W140 (1991-1998)
       "ตัว S เหลี่ยม"     "ตัว S ใหญ่ / หัวแตงโม"
```

### W201 (190E / เบบี้เบนซ์)
- **ปีผลิต:** 1982-1993 (ในไทย popular 1986-1993)
- **ตัวถัง:** Sedan
- **เครื่อง:** M102 (1.8/2.0/2.3) · M103 (2.6) · M104 (2.5-16 EVO II)
- **AMG:** 2.3-16, 2.5-16 (Cosworth — หายาก), AMG 3.2

### W202 (C-Class รุ่นแรก)
- **ปีผลิต:** 1993-2000 (ในไทย 1995-2001)
- **ตัวถัง:** Sedan, Wagon (S202)
- **เครื่อง:** M111 · M104 (2.8) · M112 (V6 — facelift)
- **AMG:** C36 AMG (M104 3.6), C43 AMG (M113 4.3 V8)

### W124 (E-Class รุ่นแรก / ตัว E เก่า)
- **ปีผลิต:** 1984-1995 (sedan), 1996 (wagon/coupe/cabrio)
- **ตัวถัง:** Sedan, Wagon (S124), Coupe (C124), Cabrio (A124)
- **เครื่อง:** M102 · M103 · M104 · M119 (V8)
- **AMG / Special:** E36, E50, E60 AMG, **500E/E500**, W124 4MATIC
- **⚠️ Signature issue:** สายไฟปี 1992-1995 (bio-degradable)

### W210 (E-Class รุ่นที่ 2 / ตัว E ตาเหยี่ยว)
- **ปีผลิต:** 1995-2002 (sedan), 1996-2003 (wagon S210)
- **ตัวถัง:** Sedan, Wagon (S210)
- **เครื่อง:** M111 · M104 (pre-facelift) · M112 V6 (facelift) · M113 V8
- **AMG / Special:** E55 AMG (M113 5.4 V8), W210 4MATIC
- **⚠️ Signature issue:** สนิม fender (front, หลังล้อหลัง)

### W126 (S-Class รุ่นที่ 2 / ตัว S เหลี่ยม)
- **ปีผลิต:** 1979-1991 (ในไทย 1985-1991)
- **ตัวถัง:** Sedan (SE/SEL), Coupe (SEC)
- **เครื่อง:** M103 · M116 (V8) · M117 (V8)
- **AMG:** 6.0 AMG "Hammer" (M117 6.0 — หายากมาก)

### W140 (S-Class รุ่นที่ 3 / ตัว S ใหญ่)
- **ปีผลิต:** 1991-1998 (ในไทย 1993-1999)
- **ตัวถัง:** Sedan (SE/SEL), Coupe (SEC → CL)
- **เครื่อง:** M104 (L6) · M119 (V8) · M120 (V12)
- **AMG / Special:** S60, S70, S73 AMG, **CL600 7.3 (Pagani)**, S600 V12
- **⚠️ Signature issues:** aux fan ไม่หมุน, soft-close door

## 📝 Required Fields

### MUST HAVE
- `chassis_code` — W201/W202/W124/W210/W126/W140
- `model_year` — int [1979-2003]
- `body_style` — sedan/wagon/coupe/cabrio
- `fuel_type` — "benzine" (ดีเซลปฏิเสธ)

### SHOULD HAVE
- `engine_displacement` — 1.8/2.0/.../6.0
- `engine_code` — M102-M120 (ระบบเดาให้)
- `engine_code_confidence` — confirmed/estimated/unknown
- `is_amg` — bool
- `amg_variant` — string (required ถ้า is_amg=true)
- `is_4matic` — bool

### NICE TO HAVE
- `mileage_km` · `transmission` · `is_facelift` · `vin_last_6` · `license_plate`

## 🧭 Decision Flow (7 ขั้น)

```
Q1: รุ่นอะไร? (190E / ตัว C / ตัว E / ตัว S / ไม่แน่ใจ)
  ↓
Q2: ปีรถ? [1979-2003]
  ↓
[System: รุ่น+ปี → chassis]
  ↓
Q3: ตัวถัง? (sedan/wagon/coupe/cabrio — limited by chassis)
  ↓
Q4: เชื้อเพลิง? (เบนซิน → ผ่าน / ดีเซล → ❌)
  ↓
Q5: ความจุเครื่อง (จาก badge)?
  ↓
Q6: เป็น AMG ไหม?
  ↓
Q7 (if W124/W210): 4MATIC หรือเปล่า?
  ↓
[System: เดา engine code → ขอยืนยัน]
  ↓
✅ PASS → §2
```

## 🗺️ Mapping Table (รุ่น+ปี → Chassis)

### "190E"
| ปี | Chassis |
|----|---------|
| 1982-1993 | W201 |
| ≥ 1994 | นอกขอบเขต |

### "ตัว C"
| ปี | Chassis |
|----|---------|
| 1993-2000 | W202 |
| ≥ 2001 | นอกขอบเขต |

### "ตัว E"
| ปี | Chassis |
|----|---------|
| 1984-1995 sedan | W124 |
| 1996 sedan | W210 |
| 1996 wagon/coupe/cabrio | W124 |
| 1996-2002 sedan | W210 |
| 1996-2003 wagon | W210 (S210) |
| ≥ 2003 | นอกขอบเขต |

### "ตัว S"
| ปี | Chassis |
|----|---------|
| 1979-1991 | W126 |
| 1991-1992 | คาบเกี่ยว — ดูภาพ |
| 1992-1998 | W140 |
| ≥ 1999 | นอกขอบเขต |

## ✅ Validation Rules

| Rule | เงื่อนไข | การกระทำ |
|------|---------|---------|
| V1 | chassis ∉ {6 ตัว} | ปฏิเสธอย่างสุภาพ |
| V2 | fuel = diesel | ปฏิเสธทันที |
| V3 | ปี + รุ่น ขัดกัน | แจ้ง + ขอภาพ |
| V4 | body style ขัด chassis | ขอตรวจสอบใหม่ |
| V5 | is_amg=true แต่ไม่ระบุ amg_variant | บังคับเลือก |
| V6 | engine guess confidence ต่ำ | mark "estimated" |
| V7 | model_year ∉ [1979, 2003] | ปฏิเสธ |

---

# §2 Symptom Intake Standard

## 🎯 วัตถุประสงค์

บันทึกอาการแบบมีโครงสร้าง — ไม่ใช่ free-text — เพื่อให้ระบบเดาอะไหล่ได้แม่น

## 🚨 หลักการ

| # | หลักการ | เหตุผล |
|---|--------|-------|
| P1 | อาการ ≠ สาเหตุ | ลูกค้ารู้อาการ ไม่รู้ root cause |
| P2 | โครงสร้าง ไม่ใช่ free-text | บังคับ category + descriptor |
| P3 | คำถามต่อยอด (conditional) | narrow down ทีละชั้น |
| P4 | ใช้ภาษาลูกค้า | "เครื่องสั่น" ไม่ใช่ "rough idle" |
| P5 | filter ตาม chassis | W124 ไม่มี SBC; W140 มี soft-close |
| P6 | severity ≠ urgency | สอง dimensions แยกกัน |

## 🗂️ Schema ของอาการ

```yaml
- id: "ENG-001"
  system: "ENG"
  label_th: "เครื่องร้อน / น้ำเดือด"
  label_tech: "engine overheating"
  chassis_filter: ["ALL"]
  severity: 5
  stop_drive_flag: true
  follow_up_questions: [...]
  likely_parts: [...]
  triage_keywords: [...]
```

## 8 หมวดอาการ (System Codes)

| Code | หมวด | ขอบเขต |
|------|------|--------|
| ENG | เครื่องยนต์ | เสียง สั่น ควัน กำลัง สตาร์ท |
| TRN | เกียร์ | กระตุก ลื่น เปลี่ยนเกียร์ |
| BRK | เบรก / ABS | เสียง ลึก สั่น ABS |
| ELC | ระบบไฟฟ้า | แบต ไฟโชว์ wiring CAN bus |
| SUS | ช่วงล่าง / พวงมาลัย | เสียง สั่น 4MATIC SLS |
| HVA | แอร์ / ระบายความร้อน | แอร์ น้ำเดือด พัดลม heater |
| BDY | ตัวถัง / ภายใน | เก้าอี้ ซันรูฟ central locking |
| LEK | น้ำมันรั่ว / ของเหลว | น้ำมัน hydraulic น้ำหล่อเย็น |

## 📋 Symptom Catalog (สรุป)

### ENG (12 อาการ)
- ENG-001 เครื่องร้อน/น้ำเดือด ⚠️ S5
- ENG-002 เครื่องสั่น/รอบเดินเบาไม่นิ่ง
- ENG-003 เครื่องดับเอง/กลางทาง ⚠️ S5
- ENG-004 สตาร์ทยาก
- ENG-005 กำลังตก/เร่งไม่ขึ้น
- ENG-006 ควันขาวออกท่อ
- ENG-007 ควันน้ำเงิน
- ENG-008 เสียงเคาะเครื่อง ⚠️ S5
- ENG-009 เสียงวาล์ว/hydraulic lifter (M104, M111)
- ENG-010 idle hunting (KE-Jet, HFM)
- ENG-011 กลิ่นน้ำมันไหม้
- ENG-012 เครื่องดับเมื่อแอร์เปิด

### TRN (7 อาการ)
- TRN-001 เกียร์กระตุก
- TRN-002 เกียร์ลื่น ⚠️ S5
- TRN-003 limp mode (722.6 — W210, W140)
- TRN-004 เกียร์ R ไม่ทำงาน
- TRN-005 เสียงเปลี่ยนเกียร์
- TRN-006 น้ำมันเกียร์รั่ว
- TRN-007 เกียร์เข้าช้า P→D (722.6)

### BRK (8 อาการ)
- BRK-001 เบรกแข็ง ⚠️ S5
- BRK-002 เบรกลึก ⚠️ S5
- BRK-003 เบรกเสียงดัง
- BRK-004 เบรกสั่น
- BRK-005 ไฟ ABS โชว์
- BRK-006 ไฟ BAS (W210, W140)
- BRK-007 เบรกมือไม่อยู่
- BRK-008 เบรกล็อก

### ELC (9 อาการ)
- ELC-001 แบตหมดบ่อย
- ELC-002 ไฟ check engine
- ELC-003 หน้าปัดดับ/mile หาย (W124/W210/W140)
- ELC-004 กระจกไฟฟ้าไม่ทำงาน
- ELC-005 ไฟส่องสว่างไม่ติด
- ELC-006 สายไฟกรอบ ⚠️ (W124 92-95, W140 early)
- ELC-007 central locking
- ELC-008 กุญแจรีโมต
- ELC-009 ไฟเตือนหลายดวง

### SUS (7 อาการ)
- SUS-001 เสียงตกหลุม
- SUS-002 พวงมาลัยสั่น
- SUS-003 พวงมาลัยหนัก/power หาย
- SUS-004 รถเอียงข้าง
- SUS-005 SLS ไม่ทำงาน (W126 SEL, W124 wagon, W140)
- SUS-006 4MATIC สั่น
- SUS-007 air susp ยุบ (W140)

### HVA (7 อาการ)
- HVA-001 แอร์ไม่เย็น
- HVA-002 แอร์เย็นข้างเดียว (W124, W140)
- HVA-003 พัดลมหม้อน้ำไม่หมุน
- HVA-004 heater ปิดไม่ได้ (W140, W210)
- HVA-005 กลิ่นเหม็นจากแอร์
- HVA-006 น้ำหยดในเก๋ง (drain ตัน)
- HVA-007 aux fan W140 ⚠️ (signature)

### BDY (6 อาการ)
- BDY-001 เก้าอี้ไฟฟ้า
- BDY-002 ซันรูฟ
- BDY-003 soft-close (W140)
- BDY-004 สนิม fender (W210 signature)
- BDY-005 กระจกหลังคาแตก
- BDY-006 ที่ปัดน้ำฝน

### LEK (6 อาการ)
- LEK-001 น้ำมันเครื่องรั่ว
- LEK-002 น้ำมันเกียร์รั่ว
- LEK-003 น้ำหล่อเย็นรั่ว
- LEK-004 hydraulic fluid รั่ว
- LEK-005 น้ำมันเบรกรั่ว ⚠️ S5
- LEK-006 น้ำเข้าเก๋ง

**รวม ~62 อาการ** (เริ่มต้น)

## 🌱 Living Catalog (ขยายได้)

### Trigger เพิ่มอาการใหม่
- ลูกค้าเลือก "อื่นๆ" + ระบุ free text
- ช่างพบอาการจริงไม่ตรงกับที่ลูกค้าเลือก
- Mr.Chuti พบ pattern ใหม่จากหลายเคส
- Engine/chassis ใหม่ที่เพิ่งรับ

### Acceptance Criteria
- เกิดในเคสจริงอย่างน้อย 2 เคส
- ไม่ใช่ duplicate
- มี follow-up questions ≥ 2
- มี likely_parts ≥ 1
- Severity ผ่านการ review

### Versioning
```
v1.0 (initial)        — 62 อาการ — 2026-05-07
v1.1 (quarterly)      — +15 อาการ
v1.2 (quarterly)      — +10 อาการ
v2.0 (major refactor) — เมื่อขยาย scope
```

### Probability Calibration 3 Phases
1. **Phase 1**: Expert estimate (ช่าง Mr.Chuti)
2. **Phase 2**: Calibrated by 50 cases
3. **Phase 3**: Calibrated by 200 cases (chassis × engine × ปี × ไมล์)

## 🔍 Conditional Questions (ตัวอย่าง)

**ENG-001 "เครื่องร้อน":**
1. เกิดเมื่อไหร่? (ติดนาน / ทางไกล / ตลอด / เป็นพักๆ)
2. น้ำหล่อเย็นลดเร็วไหม? (เร็ว / บ้าง / ไม่ลด / ไม่ทราบ)
3. เห็นน้ำที่ไหน? (ใต้ท้อง / ใต้ฝา / จากท่อ / ไม่เห็น)
4. พัดลมหม้อน้ำหมุนไหม? (หมุน / ไม่ / ช้า / ไม่ทราบ)

**ELC-006 "สายไฟกรอบ":**
1. รถคุณคือ W124 ปี 1992-1995 หรือ W140 ปีแรกๆ?
2. เห็นสายไฟกรอบ/เปลือกแตกในห้องเครื่องไหม?
3. มีไฟเตือนโชว์หลายดวงพร้อมกันไหม?
→ ถ้า Q1=ใช่ → flag "known signature issue"

## 📊 Severity Matrix

| Severity | ความหมาย | ตัวอย่าง |
|----------|---------|---------|
| 5 | อันตราย — Stop-Drive | เบรกแข็ง, น้ำมันเบรกรั่ว |
| 4 | รุนแรง — นัดด่วน 1-3 วัน | สายไฟกรอบ, น้ำหล่อเย็นรั่ว |
| 3 | ปานกลาง — นัดในสัปดาห์ | ไฟ ABS, เครื่องสั่น |
| 2 | เบา | กลิ่นแอร์, สนิม |
| 1 | cosmetic | soft-close, เก้าอี้ |

---

# §3 Safety & Stop-Drive Standard

## 🎯 วัตถุประสงค์

ป้องกันลูกค้าขับรถที่เป็นอันตรายต่อชีวิตและทรัพย์สิน

## 🚨 หลักการ

| # | หลักการ |
|---|--------|
| P1 | **Safety > Sales** — ห้ามเชียร์ขายอะไหล่ ถ้าอันตราย → บอกให้ยกรถ |
| P2 | False positive ดีกว่า false negative |
| P3 | คำเตือนต้องชัด ไม่ใช่ disclaimer |
| P4 | Stop-Drive flag ตัดสินอัตโนมัติ |
| P5 | บันทึกทุกครั้งที่เตือน (liability) |

## 🔴 5 Stop-Drive Levels

### Level 5 — IMMEDIATE STOP (หยุดทันที)
**Modal full-screen สีแดง — ห้าม dismiss**

อาการ: BRK-001, BRK-002, LEK-005, ENG-008, TRN-002, ENG-001 (extreme), ENG-003 (repeat)

```
🚨 หยุดขับทันที 🚨
[💬 LINE]  [📞 โทร]  [🚗 รถยก]
```

### Level 4 — STOP WITHIN 24H
**Banner สีส้ม sticky**

อาการ: LEK-003, ELC-006, BRK-007, ENG-006, TRN-003, HVA-003, HVA-007, BRK-008, SUS-003, ENG-011

### Level 3 — DRIVE WITH CAUTION
**Banner สีเหลือง**

อาการ: ENG-002, ENG-005, ENG-007, TRN-001, BRK-003, BRK-004, BRK-005, ELC-003, ELC-005, ELC-009, SUS-001, SUS-006, BDY-006

### Level 2 — SCHEDULED MAINTENANCE
**ไม่มี banner**

อาการ: HVA-001, HVA-005, HVA-006, ELC-007, ELC-008, BDY-002, BDY-005, LEK-001 (น้อย), LEK-006

### Level 1 — COSMETIC
**ไม่มีคำเตือน**

อาการ: BDY-001, BDY-003, BDY-004

## 🚨 Risk Combinations (รวมกัน → Level สูงขึ้น)

| Combination | ทำไมยกระดับ |
|-------------|----------|
| BRK-003 + BRK-004 | ระบบเบรกล้มเหลวซ้อนกัน |
| ENG-001 + LEK-003 | เครื่องร้อน + น้ำหล่อเย็นรั่ว = ระเบิดได้ |
| ENG-006 + LEK-003 | ควันขาว + น้ำหาย = ปะเก็นแตกแน่ |
| SUS-003 + ความเร็วสูง | พวงมาลัยหนัก ทางด่วน = อันตราย |
| ELC-006 + กลิ่นไหม้ | สายไฟกรอบ + กลิ่น = ใกล้ไฟไหม้ |
| TRN-001 + harsh shift | วาล์ว body พัง |

## 🧮 Decision Logic (pseudocode)

```python
def compute_urgency(symptoms, vehicle):
    if any(s.severity == 5 and s.stop_drive_flag for s in symptoms):
        return "STOP_DRIVE_LEVEL_5"

    if has_brake_issue() and has_steering_issue():
        return "STOP_DRIVE_LEVEL_5"
    if has_overheat() and has_coolant_leak():
        return "STOP_DRIVE_LEVEL_5"

    # Chassis-specific
    if vehicle.chassis == "W124" and 1992 <= vehicle.year <= 1995:
        if has_electrical_warning():
            return "STOP_DRIVE_LEVEL_4"

    max_severity = max(s.severity for s in symptoms)
    return level_from_severity(max_severity)
```

## ⚖️ Liability & Audit Trail

ทุกครั้งที่เตือน Stop-Drive ต้องบันทึก:
- `warning_displayed_at` (timestamp)
- `customer_acknowledgment` (accepted_tow / declined / no_response)
- `acknowledgment_at` (timestamp)
- `device_info` (browser + IP)
- `displayed_text_version`

ถ้าลูกค้า "ยอมรับความเสี่ยง" → ระบบให้บริการต่อ + แนบ disclaimer ในใบส่งต่อ

## 📊 Metrics

| Metric | เกณฑ์ดี |
|--------|---------|
| True Positive Rate | ≥ 80% |
| False Positive Rate | ≤ 15% |
| Missed Severe Cases | = 0 (เป้า) |
| Customer Compliance (Level 5) | ≥ 70% |

---

# §4 Evidence Capture Standard

## 🎯 วัตถุประสงค์

บังคับลูกค้าถ่ายภาพจุดที่เกี่ยวข้องกับอาการ — ไม่ใช่ free-form

## 🚨 หลักการ

| # | หลักการ |
|---|--------|
| P1 | บังคับถ่ายตามอาการ ไม่ใช่ free-form |
| P2 | มี example image ทุกจุด |
| P3 | ภาพ "ผ่าน" ต้องชัดและตรงจุด |
| P4 | min 2 / max 6 ภาพ |
| P5 | เก็บ metadata ทุกภาพ |
| P6 | Re-shoot ได้ ก่อน submit |

## 📋 4 Evidence Categories

### EVD-A: Vehicle Identification (3 ภาพบังคับทุกเคส)
- A1: ป้ายทะเบียน + ส่วนหน้ารถ
- A2: badge ท้ายรถ
- A3: เลขไมล์บนหน้าปัด

### EVD-B: Engine Bay (1-3 ภาพ ถ้าอาการเครื่อง/แอร์/รั่ว)
- B1: ห้องเครื่องภาพรวม
- B2: หม้อพักน้ำ / เกจน้ำ
- B3: ฝาวาล์ว / ปะเก็น

### EVD-C: Symptom-Specific (ตามอาการ)
ตัวอย่าง:
- ENG-001 → หม้อพักน้ำ + เกจอุณหภูมิ
- LEK-001 → ใต้ท้องรถ + จุดหยด
- BRK-003 → จานเบรกผ่านลายล้อ
- ELC-006 → โคลสอัพสายไฟห้องเครื่อง

### EVD-D: Optional
- รอยรั่วบนพื้น
- ห้องโดยสาร (กลิ่น/ความเสียหาย)
- OBD scanner code

## 🎬 Video & Audio Evidence

### Video (สำหรับอาการที่ต้องการ motion)
- Duration: 5-30 วินาที
- Format: MP4, MOV
- Resolution: ≥ 720p
- Audio: บังคับเปิด

ตัวอย่าง: ENG-006 ควันขาว, ENG-002 เครื่องสั่น, TRN-001 เกียร์กระตุก

### Audio-only (ENG-008 เสียงเคาะ)
- Duration: 10-20 วินาที
- Format: M4A, MP3, WAV
- Sample rate: ≥ 16 kHz

## ✅ Validation Rules (7 ข้อ)

| Rule | เงื่อนไข |
|------|---------|
| V1 | File size ≥ 100KB, ≤ 10MB (auto-compress > 5MB) |
| V2 | Resolution ≥ 800×600 |
| V3 | Aspect ratio: 4:3, 3:4, 16:9, 9:16, 1:1 |
| V4 | Format: JPG, PNG, HEIC, WebP |
| V5 | EXIF metadata บันทึก (timestamp, GPS optional) |
| V6 | Brightness/blur basic check |
| V7 | Duplicate detection |

## 🔐 Privacy & Consent

ก่อน upload — แสดง consent flow:
- ภาพใช้เพื่อวินิจฉัย + จัดอะไหล่ + บันทึกเคส
- ไม่ใช้เพื่อการตลาด/แชร์ภายนอก
- เลือกได้ว่าจะแบ่งปัน GPS หรือไม่

### Storage Retention
- 0-30 วัน: original + thumbnail
- 30-90 วัน: compressed + thumbnail
- 90+ วัน: thumbnail เท่านั้น
- 1+ ปี: ลบ (ยกเว้น case study)

## 🔧 Skip Logic (Stop-Drive Level 5)

ถ้า §3 = Level 5 → ลดภาพบังคับเหลือ EVD-A (3 ภาพ)
เพราะลูกค้าต้องรีบติดต่อ — ไม่มีเวลาถ่ายเยอะ

## 🛡️ Edge Cases

- **EC1:** ไม่มีกล้อง → upload จาก gallery หรือ skip
- **EC2:** เครื่องร้อน → "ระวังอันตราย — รอเย็นก่อน"
- **EC3:** ไม่รู้ว่าหม้อพักอยู่ที่ไหน → diagram ตำแหน่ง
- **EC4:** Network ขัด → local storage + auto-retry
- **EC5:** ภาพเก่า > 7 วัน → flag

---

# §5 Workshop Handoff Standard

## 🎯 วัตถุประสงค์

ส่งต่อเคสจาก intake → ช่างพาร์ทเนอร์ที่เหมาะสมที่สุด

## 🚨 หลักการ

| # | หลักการ |
|---|--------|
| P1 | Geo-first matching (ลูกค้าต้องการความสะดวก) |
| P2 | Skill-aware filtering |
| P3 | Workload balancing (≤ 5 active cases) |
| P4 | Transparent pricing |
| P5 | One handoff = one workshop |
| P6 | Mr.Chuti oversees (Phase 1) |
| P7 | Status visibility ทั้ง 3 ฝ่าย |

## 🗺️ Geo-Matching Algorithm

```python
def rank_candidates(case, candidates):
    scored = []
    for ws in candidates:
        score = 0
        # ใกล้ (50%)
        distance = compute_distance(case.customer, ws)
        score += 50 * max(0, (30 - distance) / 30)
        # ถนัด (25%)
        score += 25 * ws.specialty_level(case.vehicle.chassis)
        # คุณภาพ (15%)
        score += 15 * (ws.rating / 5.0)
        # ว่าง (10%)
        score += 10 * (1 - ws.active_cases / 5)
        scored.append((ws, score))
    return sorted(scored, key=lambda x: -x[1])
```

**Filters:**
- distance ≤ 30 km
- chassis ∈ workshop.specialties
- active_cases < 5
- status = "active"

**Phase 1:** ระบบเสนอ top 3 → Mr.Chuti อนุมัติ
**Phase 2:** Auto-assign top 1

## 📋 Handoff Package (3 ช่องทาง)

### 1. LINE Notification (real-time)
```
🚗 เคสใหม่ MC-2026-0042
ลูกค้า: คุณสมชาย (081-xxx-xxxx)
รถ: W140 S320 ปี 1995 sedan
ตำแหน่ง: จตุจักร (8.2 km)
อาการ: ENG-001 ⚠️ Level 4
อะไหล่ที่จัด: หม้อน้ำ + ปั๊มน้ำ + thermostat
ค่าแรงประมาณ: 2,500-3,500
[ดู PDF] [✅ รับ] [❌ ปฏิเสธ]
```

### 2. Google Sheet (centralized)
แถวใหม่ใน "Workshop Handoffs":
handoff_id, case_id, customer info, vehicle, symptom, urgency, workshop_id, status, timestamps...

### 3. PDF Handoff Document (formal, 1-2 หน้า)
- ข้อมูลลูกค้า + รถ + อาการ
- ภาพประกอบทั้งหมด (จาก §4)
- ผลวินิจฉัย + likely_parts
- อะไหล่ที่ Mr.Chuti จัดไว้ (ราคา)
- ค่าแรงประมาณ
- คำเตือนเฉพาะรุ่น
- ลายเซ็นข้อตกลง

## 🔄 Lifecycle (9 สถานะ)

```
1. PENDING_ASSIGNMENT   (Mr.Chuti กำลังเลือกช่าง)
2. ASSIGNED             (ส่งช่างแล้ว — รอ accept)
3. ACCEPTED             (ช่างรับงาน)
4. SCHEDULED            (ลูกค้านัดวัน)
5. IN_PROGRESS          (ช่างกำลังซ่อม)
6. PARTS_NEEDED         (ขออะไหล่เพิ่ม — optional loop)
7. COMPLETED            (ซ่อมเสร็จ)
8. DELIVERED            (ลูกค้ารับรถ)
9. CLOSED               (ปิดเคส — ส่งต่อ §6)
```

### Timeout Rules

| State | Timeout | Action |
|-------|---------|--------|
| ASSIGNED | 24 ชม. (12 ชม. ถ้า Stop-Drive 4+) | Re-assign |
| ACCEPTED → SCHEDULED | 48 ชม. | Mr.Chuti follow up |
| SCHEDULED → IN_PROGRESS | 7 วัน | Reminder ทั้งคู่ |
| IN_PROGRESS → COMPLETED | 14 วัน | Mr.Chuti โทรเช็ค |
| COMPLETED → DELIVERED | 30 วัน | Auto-close + flag |

## 💰 Revenue Model

```
Customer pays:
  ค่าอะไหล่ (จ่าย Mr.Chuti)        5,900
  ค่าแรง (จ่ายช่างโดยตรง)         3,000
  ค่าบริการ Mr.Chuti (optional)     200
  ───────────────────────────────────────
  รวม                              9,100

Mr.Chuti revenue:
  + ค่าอะไหล่     5,900
  + ค่าบริการ       200
  + Referral 5%     150
  ─────────────────────
  รวม              6,250

Workshop revenue:
  + ค่าแรง        3,000
  - Referral 5%    -150
  ─────────────────────
  รวม              2,850
```

### Referral Phases
| Phase | % | หมายเหตุ |
|-------|---|---------|
| 1 (เริ่มต้น) | 5% | จูงใจช่างเข้าร่วม |
| 2 (ติดตลาด) | 7-10% | network value เพิ่ม |
| 3 (mature) | 10-15% | brand premium |

## 🚨 Edge Cases

- **EC1:** ไม่มีช่างใกล้ (>30km) → เสนอ 2 ทาง: ขายอะไหล่อย่างเดียว / มาที่ Mr.Chuti
- **EC2:** ช่างปฏิเสธทั้ง top 3 → re-rank top 4-6 → manual contact
- **EC3:** ลูกค้าไม่พอใจช่าง → re-match (บันทึก) → ถ้าซ้ำ 2 ครั้ง flag ช่างเก่า
- **EC4:** ช่างพบอาการเพิ่ม → PARTS_NEEDED state → Mr.Chuti จัดเพิ่ม → ลูกค้า approve
- **EC5:** Stop-Drive Level 5 + ห่างไกล → รถยก Mr.Chuti partner → อู่ที่ Mr.Chuti เลือก

---

# §5-Sup Workshop Registration Standard

## 🎯 วัตถุประสงค์

กระบวนการรับสมัคร verify และจัดการอู่พาร์ทเนอร์

## 📋 Workshop Profile Schema

### MUST HAVE
- workshop_id, name, owner info, address, geo coords
- business_hours, specialties (chassis), years_experience
- verification_status

### SHOULD HAVE
- workshop_size, tools_available, engine_specialties
- service_types, bank_account, tax_id, line_id

### COMPUTED (จากระบบ)
- rating (avg จาก §6), total_cases, success_rate
- avg_completion_days, active_cases, last_active

## 🔐 Vetting Process (5 Stages)

```
1. APPLIED          → submit form (ที่อยู่ + GPS + ภาพอู่ + อ้างอิง)
2. DOCUMENT_REVIEW  → Mr.Chuti ตรวจเอกสาร
3. INTERVIEW        → โทร/เยี่ยมอู่
4. TRIAL (5 cases)  → average rating ≥ 4.0
5. VERIFIED         → full member + badge
```

## 📊 KPIs (ทุกเดือน)

| KPI | เกณฑ์ดี | Action ถ้าต่ำ |
|-----|---------|--------------|
| Customer Rating | ≥ 4.0 | warning ที่ 3.5, suspend ที่ 3.0 |
| Acceptance Rate | ≥ 70% | สอบถามสาเหตุ |
| On-time Delivery | ≥ 80% | review workload |
| Referral Payment | 100% | flag, dispute |
| Re-work Rate | ≤ 10% | retraining |
| Customer Complaints | 0-1/เดือน | investigate ทันที |

## 🏆 Tier System (Phase 2)

```
🥉 Bronze (เริ่มต้น)
   - Trial passed
   - 5-20 เคส/เดือน
   - referral 5%

🥈 Silver
   - 6 เดือน + rating ≥ 4.2
   - 20-50 เคส/เดือน
   - referral 7%

🥇 Gold
   - 1 ปี + rating ≥ 4.5
   - 50+ เคส/เดือน
   - referral 5% (ลด)
   - priority assignment + co-marketing
```

## ⚠️ Suspension Rules

| สถานการณ์ | Action |
|----------|--------|
| Rating < 3.0 (5 เคสติดกัน) | Auto-suspend 30 วัน |
| Customer complaint รุนแรง | Auto-suspend + investigation |
| ค้างจ่าย referral > 60 วัน | Suspend จนจ่าย |
| Inactive > 90 วัน | Mark inactive |
| ปลอมเอกสาร | Permanent ban |

## 📝 Onboarding Document
- Workshop Partner Handbook
- Pricing Guideline
- Communication Standards (LINE response ≤ 4 ชม.)
- Legal Contract (1 ปี ต่ออายุได้)

---

# §6 Outcome Verification Standard

## 🎯 วัตถุประสงค์

ปิดวงจรเคส + เก็บ feedback 3 ฝ่าย → feedback loop กลับ §1-§5

## 🚨 หลักการ

| # | หลักการ |
|---|--------|
| P1 | Triangulation จาก 3 ฝ่าย (ลด bias) |
| P2 | Quantitative + Qualitative |
| P3 | Feedback ที่ actionable |
| P4 | Feedback loop กลับโดยอัตโนมัติ |
| P5 | Time-bounded (7 วัน) |
| P6 | Anonymized when needed |
| P7 | Closing > Verification |

## 👥 3 ฝ่าย Feedback

### 🟢 Customer Feedback (4 sections)
1. **Workshop Service** — rating, on-time, อาการหาย, ราคา, แนะนำเพื่อน
2. **Parts Quality** — คุณภาพ, ปัญหาหลังเปลี่ยน, เทียบร้านอื่น
3. **Mr.Chuti Overall** — ความง่ายฟอร์ม, การจับคู่, คะแนนรวม, จะใช้อีกไหม
4. **Open Feedback** — ข้อเสนอแนะ

**Reward:** ส่วนลด 5% สำหรับเคสถัดไป

### 🔵 Workshop Feedback (5 sections)
1. **Customer Quality** — ความร่วมมือ, ตรงเวลา, จ่ายเงิน
2. **Intake Form Quality** ⭐ — ตรง? + อาการที่เจอเพิ่ม + ข้อมูลรถถูกไหม + รูปใช้ได้ไหม
3. **Diagnosis Accuracy** — อะไหล่ใช้กี่ชิ้น, root cause จริง, likely_parts ตรงไหม
4. **Mr.Chuti Service** — ประสานงาน, ความเร็ว, referral fee
5. **Open Feedback**

### 🟠 Mr.Chuti Internal Review (4 sections)
1. **Case Health Check** — ปิดสะอาด? cycle time, ค่าแรง variance
2. **Diagnosis Accuracy Score** — §2 prediction, §3 safety level, §5 matching
3. **Revenue Validation** — รายได้, margin, referral status
4. **Catalog Improvement Flags**

## 🔄 5 Feedback Loops

### Loop 1: Catalog Calibration (§2 + §6)
```
Mr.Chuti flag "เพิ่ม symptom ใหม่"
  → flag ซ้ำ ≥ 2 เคส
  → เพิ่มเข้า catalog v1.x
  → ฟอร์มใหม่ใช้ catalog ใหม่
```

### Loop 2: Probability Calibration (§2 likely_parts)
```
ทุก 50 เคสของ symptom + chassis เดียวกัน:
  if |actual - predicted| > 15%
    → flag for review
    → ปรับค่า (gradual, ไม่กระโดด)
```

### Loop 3: Workshop Performance (§5-Sup)
```
ทุก 10 เคสของช่าง:
  update rating, on-time, re-work
  → trigger warning/suspend ถ้าต่ำ
```

### Loop 4: Safety False Positive (§3)
```
จาก Mr.Chuti review:
  count(over-warned) / count(total) → FPR
  if FPR > 15% สำหรับอาการ X
    → review Stop-Drive rule
    → ปรับ severity
    → ทดสอบใน 50 เคสถัดไป
```

### Loop 5: Customer Trust Score (brand health)
```
Composite score จาก:
  - "ใช้อีกไหม" (loyalty)
  - "แนะนำเพื่อน" (NPS-like)
  - คะแนนรวม
→ Track ทุกเดือน
→ ถ้าลด > 10% → emergency review
```

## 📊 KPIs Dashboard

### Operational (รายวัน)
- Active cases, Avg cycle time, Stop-Drive escalations, Workshop accept rate

### Quality (รายสัปดาห์)
- Customer satisfaction ≥ 4.3
- Workshop satisfaction ≥ 4.0
- Diagnosis accuracy ≥ 65%
- Re-work rate ≤ 10%

### Business (รายเดือน)
- Revenue per case, Repeat customer rate ≥ 25%
- NPS ≥ 30, Workshop retention ≥ 90%

### Catalog Health (รายไตรมาส)
- Catalog coverage ≥ 90%
- New symptoms added, Probability drift

## ⚖️ Dispute Resolution

| Dispute | Resolution |
|---------|-----------|
| ไม่หายตามที่อ้าง | นัด re-check + รับผิดชอบร่วม |
| ราคาเกิน | ตรวจ PARTS_NEEDED log |
| คุณภาพอะไหล่ | warranty check + Mr.Chuti รับผิดชอบ |

**Resolution Framework:**
1. Listen ทั้ง 2 ฝ่าย (≤ 48 ชม.)
2. Review evidence (§4, §5 PDF, work log)
3. Apply: ลูกค้าถูกจนกว่าจะพิสูจน์เป็นอย่างอื่น
4. Outcomes: ลูกค้าผิด / ช่างผิด / Mr.Chuti ผิด / 50/50

## 🎯 Long-term Vision

| Phase | เดือน | Capabilities |
|-------|------|--------------|
| 1 | 1-3 | Basic Dashboard + Manual review |
| 2 | 3-6 | Pattern Recognition + Auto-flag |
| 3 | 6-12 | Predictive Insights |
| 4 | 1+ ปี | Self-Tuning |

---

# Implementation Roadmap

## Phase 1: MVP Customer Form (เดือน 1-2)
**Standards:** §1, §2, §3, §4
**Deliverable:** ปรับปรุง `chutiparts.github.io/intake/` ให้ตาม §1-§4

**Concrete tasks:**
- [ ] Update intake form: 6 chassis + AMG + 4MATIC fields
- [ ] Implement decision tree §1
- [ ] Add 62 symptoms catalog (initial)
- [ ] Add conditional questions
- [ ] Add Stop-Drive warning logic
- [ ] Add evidence capture (camera + validation)
- [ ] Update Apps Script ให้รองรับ schema ใหม่
- [ ] Update Google Sheet columns

## Phase 2: Workshop Network (เดือน 2-3)
**Standards:** §5, §5-Sup
**Deliverable:** Workshop portal + LINE integration + PDF generator

**Concrete tasks:**
- [ ] สร้าง Workshop Registration form
- [ ] ตรวจสอบ + onboard ช่าง 3-5 อู่แรก
- [ ] เซ็นสัญญา Partner
- [ ] Implement geo-matching algorithm
- [ ] LINE Notify integration
- [ ] PDF generator (handoff document)
- [ ] Workshop dashboard (Sheet-based)

## Phase 3: Outcome & Feedback (เดือน 3-4)
**Standards:** §6
**Deliverable:** Feedback collection + Sheet automation

**Concrete tasks:**
- [ ] Customer feedback form (LINE 3 วันหลัง DELIVERED)
- [ ] Workshop feedback form (ก่อนรับ referral)
- [ ] Mr.Chuti review form
- [ ] Dispute resolution workflow

## Phase 4: Feedback Loops (เดือน 4-6)
**Deliverable:** Catalog calibration + KPIs dashboard

**Concrete tasks:**
- [ ] Loop 1-5 implement (semi-automated)
- [ ] KPIs dashboard (Sheet → Looker Studio)
- [ ] Catalog versioning
- [ ] Quarterly review cadence

## Phase 5: Optimization (เดือน 6+)
- ML-assisted predictions
- Predictive maintenance suggestions
- Scaling beyond Bangkok

---

# Appendices

## Appendix A: Status Codes Reference

### Case Lifecycle (§5)
| Code | สถานะ |
|------|------|
| 1 | PENDING_ASSIGNMENT |
| 2 | ASSIGNED |
| 3 | ACCEPTED |
| 4 | SCHEDULED |
| 5 | IN_PROGRESS |
| 6 | PARTS_NEEDED |
| 7 | COMPLETED |
| 8 | DELIVERED |
| 9 | CLOSED |

### Workshop Status (§5-Sup)
| Code | สถานะ |
|------|------|
| 1 | APPLIED |
| 2 | DOCUMENT_REVIEW |
| 3 | INTERVIEW |
| 4 | TRIAL |
| 5 | VERIFIED |
| 6 | WARNING |
| 7 | SUSPENDED |
| 8 | REINSTATED / REMOVED |

## Appendix B: Symptom Code Format

```
[SYSTEM]-[NUMBER]
   |        |
   |        └── 001-999 (running number)
   └── ENG/TRN/BRK/ELC/SUS/HVA/BDY/LEK
```

## Appendix C: Engine Code Reference

| Code | ประเภท | Used in |
|------|-------|---------|
| M102 | L4 SOHC 2.0/2.3 | W201, W124 |
| M103 | L6 SOHC 2.6/3.0 | W201, W124, W126 |
| M104 | L6 DOHC 2.8/3.2/3.6 | W124, W202, W210, W140 |
| M111 | L4 DOHC 1.8/2.0/2.2/2.3 | W202, W210 |
| M112 | V6 DOHC 2.4-3.7 | W202 facelift, W210 facelift |
| M113 | V8 DOHC 4.3/5.0/5.4 | W210 |
| M116 | V8 SOHC 3.8/4.2 | W126 |
| M117 | V8 SOHC 4.5/5.0/5.6 | W126 |
| M119 | V8 DOHC 4.2/5.0 | W124, W140 |
| M120 | V12 DOHC 6.0 | W140 |

## Appendix D: Out of Scope (ปฏิเสธอย่างสุภาพ)

| เคส | ข้อความ |
|-----|--------|
| ดีเซล | "Mr.Chuti รับเฉพาะเครื่องเบนซินครับ" |
| W123 | "Mr.Chuti เริ่มที่ W201/W124 (1982+)" |
| W203/W211/W220 | "ยังไม่รับรุ่นใหม่กว่านี้ครับ" |
| ไม่ใช่ MB | "Mr.Chuti เชี่ยวชาญ Mercedes-Benz เท่านั้น" |

## Appendix E: Document History

| Version | วันที่ | สรุป |
|---------|-------|------|
| 1.0 | 2026-05-07 | Initial complete release — §1 ถึง §6 + §5-Sup |

---

## 🎉 MPTS-1 Standard Suite COMPLETE

**โครงสร้าง 6+1 standards:**
- §1 Vehicle Identity
- §2 Symptom Intake
- §3 Safety & Stop-Drive
- §4 Evidence Capture
- §5 Workshop Handoff
- §5-Sup Workshop Registration
- §6 Outcome Verification

**ครอบคลุม end-to-end:**
ลูกค้าแจ้ง → วินิจฉัย → ภาพ → จับคู่ช่าง → ซ่อม → feedback → เรียนรู้

**พร้อม implement:**
Phase 1 (เดือน 1-2) → Phase 5 (เดือน 6+)

---

**Mr.Chuti อะไหล่ Mercedes-Benz มือสอง**
LINE: @mr.chuti5988
ฟอร์ม: chutiparts.github.io/intake/

**END OF MPTS-1 v1.0 (Complete)**
