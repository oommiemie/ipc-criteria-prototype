# IPC Criteria Form — Herbal ERP Prototype

> **Single-file React prototype** สำหรับหน้า "สร้าง IPC Criteria ใหม่" ในระบบ Herbal ERP ที่ใช้ในโรงงานยาสมุนไพร — รองรับการกำหนดเกณฑ์ควบคุมคุณภาพในกระบวนการผลิต (In-Process Control) ตามหลัก GMP / USP

🌐 **Live Demo:** https://oommiemie.github.io/ipc-criteria-prototype/

---

## ✨ Features

### 🎯 Smart Auto-fill
- เลือก **Test Name** จากมาตรฐาน USP → ระบบเติม Code, Unit, Sample Size, Tolerance, Critical flag ให้อัตโนมัติ
- รองรับ 25+ หัวข้อทดสอบมาตรฐาน (Weight Variation, Dissolution, Hardness, Friability, Disintegration, Assay, ฯลฯ)

### 🧪 Type-specific Forms
ฟอร์มเปลี่ยนตามประเภทเกณฑ์ที่เลือก:
- **Numeric** — Target ± Tolerance, คำนวณ Min/Max อัตโนมัติ
- **Pass / Fail** — กำหนดเกณฑ์ผ่าน/ไม่ผ่าน + default expected
- **Visual** — checklist ที่ต้องตรวจ + รูปอ้างอิง
- **Text** — รูปแบบและตัวอย่างที่คาดหวัง

### 🔁 Multi-Stage Acceptance (GMP)
ตามหลัก USP `<711>` (Dissolution) และ `<905>` (Uniformity) :
- Stage 1 → ถ้า fail → Stage 2 (สุ่มเพิ่ม) → ถ้ายัง fail → Reject / Deviation
- คำนวณ "ยอมเสียได้" และ "ต้องผ่านขั้นต่ำ" อัตโนมัติแยกตามขั้น
- แต่ละ Stage เลือก action ได้: Next Stage, Reject Batch, บันทึก Deviation

### 🔍 Searchable Dropdowns + Custom Options
- ทุก dropdown ค้นหาด้วย keyboard ได้ (highlight ผลลัพธ์)
- ตัวเลือกที่ไม่มี → เพิ่มเองได้ผ่าน popup modal
- รองรับ keyboard shortcuts: ↑↓ Enter Esc

### 👁 Live Preview Panel (Sticky)
- แสดงตัวอย่าง criteria ที่ operator จะเห็นจริง — อัปเดต real-time
- รวม Acceptance Flow diagram ตามจำนวน stage

### 📱 Responsive Design
- Mobile (<640px): single column + hamburger sidebar
- Tablet (640–1280px): 2 columns + preview ลงล่าง
- Desktop (1280px+): 2 columns + preview ขวา sticky

---

## 🛠 Tech Stack

| ส่วน | ใช้อะไร |
|---|---|
| Framework | React 18 (UMD via CDN) |
| Styling | Tailwind CSS (Play CDN) + Custom CSS variables |
| Build | ❌ ไม่ต้องบิวด์ — เปิดไฟล์ HTML ในเบราว์เซอร์ได้ทันที |
| Transpile | Babel Standalone (in-browser JSX) |
| State | React `useState` + `useRef` + `useEffect` |
| Fonts | Inter + Sarabun (Google Fonts) |

---

## 🚀 วิธีรัน

```bash
# Clone
git clone https://github.com/oommiemie/ipc-criteria-prototype.git
cd ipc-criteria-prototype

# เปิดได้เลย (Mac)
open index.html
```

หรือ double-click ไฟล์ `index.html` ก็ได้ — ไม่ต้องลง dependencies

---

## 📝 Prompts ที่ใช้สร้างหน้านี้ (ตามลำดับ)

> README ส่วนนี้บันทึก prompt ทุก turn ที่ใช้สร้างจนได้ผลงานนี้ — สามารถใช้เป็น reference สำหรับงาน prompt engineering หรือสร้างหน้าคล้ายกันได้

### 🟢 Step 1 — สร้างโครงเริ่มต้น

**Prompt:**
> ช่วยออกแบบหน้าข้อมูลตามนี้ สร้างเป็น react ขอเป็น prototype แค่หน้าจอเดียว
> *(แนบรูป screenshot จาก https://herbal-erp-metaherb.bmscloud.in.th)*

**ผลลัพธ์:**
- Single HTML file ใช้ React + Tailwind via CDN
- Sidebar ของ Herbal ERP (Production > Master Data active)
- Form panel ฟิลด์ครบตามภาพ: Code, Unit, Dosage Form, Criteria Type, Test Name, Target/Tolerance, Min/Max, Sample Size, Critical/Active toggles

### 🟢 Step 2 — เพิ่ม Multi-Stage GMP Retest

**Prompt:**
> กำหนดเงื่อนไข สุ่ม sample size และกำหนด Sample Failure Tolerance ±% เมื่อครั้งไม่ผ่านให้สามารถกำหนดเงื่อนไขครั้งที่ 2 ตามหลักการของ GMP

**ผลลัพธ์:**
- เพิ่ม panel "Sampling Plan" + "Multi-Stage Acceptance Criteria"
- รองรับ Stage 1, 2, 3 ตาม USP `<711>`, `<905>`
- แต่ละ stage มี Sample Size, Average Tolerance, Individual Limit, On-Fail action

### 🟢 Step 3 — ลองเวอร์ชันง่ายที่สุด → กลับมาแบบเดิม

**Prompt:**
> ขอให้ใช้งานง่ายที่สุด → ขอแบบเมื่อกี้

**ผลลัพธ์:**
- ทดลองตัดเหลือ 2 step (สุ่ม N ชิ้น, ยอมเสียได้ M ชิ้น)
- ตัดสินใจกลับไปใช้แบบเดิมที่มี 3 stages เพราะใกล้เคียงมาตรฐาน USP จริง

### 🟢 Step 4 — บันทึกไฟล์ + เปลี่ยน Unit เป็น Dropdown

**Prompts:**
> ช่วย save file html ให้หน่อย จะไปเปิดเครื่องอื่น
>
> Unit เปลี่ยนเป็น dropdown

**ผลลัพธ์:**
- คัดลอกไฟล์ไป Desktop
- Unit dropdown มี 20 หน่วยมาตรฐาน (mg, g, mm, ml, °C, pH, ฯลฯ)

### 🟢 Step 5 — Form ปรับตาม Criteria Type

**Prompt:**
> ประเภทเกณฑ์ (Criteria Type)* ปรับรูปแบบ form การบันทึกข้อมูลตามการเลือกประเภท

**ผลลัพธ์:**
- 4 รูปแบบ: Numeric / Pass-Fail / Visual / Text
- Banner สีต่างกันบอกประเภทที่กำลังบันทึก
- ฟิลด์ที่แสดงเปลี่ยนตามประเภทเลย

### 🟢 Step 6 — ลบฟิลด์ไม่จำเป็น + คำนวณ Min/Max อัตโนมัติ

**Prompts:**
> Specification Description (Optional), Test Method เอาออก
>
> เมื่อทำการกรอกข้อมูลในส่วนของ Specification Target & Tolerance ให้คำนวณค่า min-max value ให้อัตโนมัติ

**ผลลัพธ์:**
- ลบฟิลด์ที่ไม่ค่อยใช้
- Min/Max readonly คำนวณจาก `Target ± Tolerance%`
- มีแถบสรุป `285 ≤ value ≤ 315 (300 ± 5%)`

### 🟢 Step 7 — Dropdown สร้างตัวเลือกเองได้

**Prompts:**
> Sampling Method สามารถเพิ่มตัวเลือกหรือสร้างเองได้
>
> เปลี่ยนเป็นให้มีกดเพิ่มจากใน dropdown เลย แล้วแสดง popup ขึ้นให้กรอกข้อมูลแทน

**ผลลัพธ์:**
- สร้าง `EditableSelect` component แบบ generic
- Modal popup เด้งขึ้นกลางจอเมื่อเลือก `＋ เพิ่มตัวเลือกใหม่...`
- รองรับ field config (name, description, reference, ฯลฯ)
- Keyboard: Enter = บันทึก, Esc = ยกเลิก

### 🟢 Step 8 — ลบ Individual Limit + เปลี่ยน QA Review เป็น Deviation

**Prompts:**
> เอา Individual Limit ±% ออก
>
> เปลี่ยนจาก ⚑ ส่ง QA Review เป็นการแสดง deviation

**ผลลัพธ์:**
- Stage card เหลือ 2 ฟิลด์: Sample Size, Tolerance
- เพิ่ม Deviation preview card (DEV-2026-XXXX, Severity, Status, Assignee)
- ตามหลัก ICH Q9 / Q10 Quality Risk Management

### 🟢 Step 9 — Dosage Form มาตรฐาน + ตัวเลือกเอง

**Prompt:**
> รูปแบบยา (Dosage Form) ยามาตรฐาน และสามารถสร้างตัวเลือกเองได้ด้วย

**ผลลัพธ์:**
- 29 รูปแบบยามาตรฐาน (Tablet, Capsule, Pill/Bolus, Tincture, Decoction, Balm, Patch, Tea Bag, ฯลฯ)
- รวมรูปแบบยาไทย/สมุนไพรเฉพาะ

### 🟢 Step 10 — คำนวณ "ยอมเสียได้" อัตโนมัติแต่ละ Stage

**Prompts:**
> เมื่อทำการกรอกข้อมูล Sample Size และ Tolerance ±% ให้คำนวณจำนวนให้ด้วย
>
> ไม่ต้องคำนวณรวม stage กัน ให้แยก stage ของตัวเองเลย

**ผลลัพธ์:**
- 3 ช่องสรุปต่อ stage: ทดสอบ N ชิ้น, ยอมเสียได้ M ชิ้น, ต้องผ่าน (N-M) ชิ้น
- สูตร: `floor(SampleSize × Tolerance%)` แยกต่อ stage

### 🟢 Step 11 — Test Name ตัวเลือกเอง + ค้นหาได้

**Prompts:**
> หัวข้อการทดสอบ (Test Name)* สามารถสร้างตัวเลือกเองได้ด้วย
>
> ขอให้สามารถค้นหาตัวเลือกได้

**ผลลัพธ์:**
- 25 หัวข้อทดสอบมาตรฐาน (Physical / Chemical / Microbio / Herbal-specific)
- สร้าง `SearchableSelect` แทน native `<select>`
- ค้นหาแบบ real-time พร้อม highlight match (สีเหลือง)
- Keyboard: ↑↓ เลื่อน, Enter เลือก, Esc ปิด

### 🟢 Step 12 — UI/UX ใหญ่: Sections + Auto-fill + Sticky Footer

**Prompt:**
> ปรับ UI ให้ดู user-friendly ดูข้อมูลบันทึกข้อมูลง่าย ตรงไหนที่สามารถเพิ่มข้อมูลในช่องให้อัตโนมัติได้

**ผลลัพธ์:**
- แบ่งเป็น 4 sections มีหัวข้อหมายเลข: Basic / Specification / Sampling / Settings
- **Smart auto-fill from Test Name**:
  - Code: `IPC-{prefix}-{seq}` (เช่น Weight → IPC-WV-742)
  - Unit: ตามมาตรฐาน USP
  - Sample Size + Tolerance + Stages: USP recommended
  - Critical: true สำหรับ Sterility, Heavy Metals, Assay
- Auto badge `⚡ Auto` บนช่องที่ถูกเติม
- Notification "เติมให้อัตโนมัติ: Code · Unit · Sample Plan"
- Sticky footer พร้อม status indicator
- Toggle cards สำหรับ Critical / Active

### 🟢 Step 13 — ลอง Templates + Live Preview + Auto-save → กลับเหลือ Live Preview

**Prompts:**
> มีอะไรแนะนำอีกใหม่เกี่ยวกับ ui → ลองทำให้ให้หน่อย
>
> ขอแบบเดิม แต่ยังคงมี Live Preview (และเปลี่ยนไอคอนใหม่ด้วย)

**ผลลัพธ์:**
- ทดลองเพิ่ม: Templates Bar (USP presets) + Progress Bar + Auto-save Draft
- ตัดสินใจเก็บไว้แค่ **Live Preview Panel** (ขวามือ sticky)
- เปลี่ยนไอคอน Live Preview เป็น SVG monitor ดีไซน์เอง + จุดเขียวกระพริบ

### 🟢 Step 14 — Responsive Design

**Prompt:**
> ปรับให้รองรับการแสดงผล responsive

**ผลลัพธ์:**
- Sidebar ซ่อนใน mobile + ปุ่ม hamburger ☰
- Sidebar slide-in พร้อม backdrop
- Form grids ทุกชุด `grid-cols-1 sm:grid-cols-2`
- Header / footer / preview ปรับตาม breakpoint
- ทำงานดีตั้งแต่ 320px ถึง 4K

---

## 🧩 Architecture

```
┌─────────────────────────────────────────────────────────┐
│ index.html (single file, ~1700 lines)                    │
├─────────────────────────────────────────────────────────┤
│  CDN: React 18, Tailwind, Babel Standalone, Google Fonts │
│  Custom CSS: variables, panels, toggles, scrollbar       │
├─────────────────────────────────────────────────────────┤
│  Components:                                              │
│   • Icon          — SVG icon library                      │
│   • Sidebar       — Nav with mobile drawer                │
│   • Toggle        — Custom switch                         │
│   • SearchableSelect — Dropdown + search + add-new        │
│   • EditableSelect   — Wraps SearchableSelect + modal     │
│   • AddOptionModal   — Generic field-driven modal         │
│   • App           — Form state + sections + preview       │
└─────────────────────────────────────────────────────────┘
```

### Key State Patterns
- `form` — single state object (ทุกฟิลด์)
- `autoFilled` — Set ของ field keys ที่ถูก auto-fill (สำหรับ badge)
- `dosageForms`, `testNames`, `samplingMethods` — useState (เพิ่มเองได้)
- `mobileNavOpen` — sidebar drawer state
- `testMetadata` — mapping จาก test value → defaults (prefix, unit, stages, etc.)

---

## 📖 References ที่ใช้

- USP `<711>` Dissolution
- USP `<905>` Uniformity of Dosage Units
- USP `<1216>` Tablet Friability
- USP `<701>` Disintegration
- ICH Q9 — Quality Risk Management
- ICH Q10 — Pharmaceutical Quality System

---

## 📄 License

MIT — ใช้เป็น reference ฟรี

## 👥 Credits

- Designed & built by Claude (Anthropic) ผ่าน Claude Code
- For oommiemie / Herbal ERP project
