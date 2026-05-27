# Exapilot Studio — คู่มือการใช้งาน

> **SOP Automation Builder** สำหรับออกแบบ ทดสอบ และจำลองการทำงานของ Procedure ในระบบ DCS (Distributed Control System)

🌐 **ใช้งานออนไลน์ได้เลย:** [https://supasiao7896th.github.io/Exapilot-Studio/](https://supasiao7896th.github.io/Exapilot-Studio/)

---

## สารบัญ

1. [ภาพรวม](#1-ภาพรวม)
2. [การเริ่มต้นใช้งาน](#2-การเริ่มต้นใช้งาน)
3. [ส่วนประกอบของหน้าจอ](#3-ส่วนประกอบของหน้าจอ)
4. [Block ทั้งหมด](#4-block-ทั้งหมด)
5. [การเชื่อมต่อเส้น (Edge)](#5-การเชื่อมต่อเส้น-edge)
6. [แท็บ Properties, Tags และ Coach](#6-แท็บ-properties-tags-และ-coach)
7. [Auto-Generate Wizard](#7-auto-generate-wizard)
8. [การจำลองการทำงาน (Run)](#8-การจำลองการทำงาน-run)
9. [การบันทึกและโหลด Procedure](#9-การบันทึกและโหลด-procedure)
10. [Approval Sheet (ใบขออนุมัติ)](#10-approval-sheet-ใบขออนุมัติ)
11. [Keyboard Shortcuts](#11-keyboard-shortcuts)
12. [เคล็ดลับการใช้งาน](#12-เคล็ดลับการใช้งาน)

---

## 1. ภาพรวม

Exapilot Studio เป็น Web Application แบบ **Single File** (ไม่ต้องติดตั้ง, ไม่ต้องเชื่อมต่อ Server) ใช้สำหรับ:

- 🗺️ **ออกแบบ Flowchart** ของ SOP (Standard Operating Procedure)
- ⚙️ **กำหนด Logic** เงื่อนไข, Timer, Output ไปยัง DCS Tag
- 🏃 **จำลองการทำงาน** ของ Procedure แบบ Step-by-Step
- ✅ **ตรวจสอบความถูกต้อง** ด้วย Coach Validator ก่อน Deploy จริง
- 📋 **สร้างใบขออนุมัติ** (PE-F-0054-03) พร้อมรายการขั้นตอนอัตโนมัติจาก Flowchart

---

## 2. การเริ่มต้นใช้งาน

### วิธีที่ 1 — เปิดผ่านเว็บ (ง่ายที่สุด)
เปิด Browser แล้วไปที่:
```
https://supasiao7896th.github.io/Exapilot-Studio/
```

### วิธีที่ 2 — เปิดไฟล์ในเครื่อง
1. ดาวน์โหลดไฟล์ `index.html` จาก GitHub
2. ดับเบิลคลิกเพื่อเปิดใน Browser (Chrome / Edge แนะนำ)
3. ไม่ต้องติดตั้งอะไรเพิ่ม ✅

### เริ่มสร้าง Procedure ใหม่
- **ลาก Block** จาก Palette ทางซ้ายมาวางบน Canvas
- หรือกด **`ตัวอย่าง`** เพื่อโหลด Procedure ตัวอย่างสำเร็จรูป
- หรือใช้ **Auto-Generate Wizard** (ปุ่ม ✦ Auto-Generate) สร้างอัตโนมัติ

---

## 3. ส่วนประกอบของหน้าจอ

```
┌─────────────────────────────────────────────────────────────┐
│  TOOLBAR (แถบด้านบน)                                        │
│  [ชื่อ Procedure] [READY] [▶ Run] [Reset] [Speed] [Save]..  │
├──────────────┬──────────────────────────────┬───────────────┤
│              │                              │  Properties   │
│   PALETTE    │        CANVAS                │  Tags         │
│  (Block ทั้ง  │   (พื้นที่วาด Flowchart)      │  Coach        │
│   หมด)       │                              │               │
│              │                              │               │
├──────────────┴──────────────────────────────┴───────────────┤
│  EXECUTION CONSOLE (log การทำงานขณะ Run)                    │
└─────────────────────────────────────────────────────────────┘
```

### Toolbar
| ปุ่ม | หน้าที่ |
|------|---------|
| **ชื่อ Procedure** | คลิกเพื่อแก้ไขชื่อ |
| **READY / RUNNING / PAUSED** | สถานะปัจจุบัน |
| **▶ Run** | เริ่มจำลองการทำงาน |
| **Reset** | หยุดและรีเซ็ตกลับสู่สถานะเริ่มต้น |
| **Speed** | ความเร็วจำลอง: 1x / 2x / 4x / 8x |
| **✦ Auto-Generate** | สร้าง Flowchart อัตโนมัติจาก Wizard |
| **ตัวอย่าง** | โหลด Procedure ตัวอย่าง |
| **📋 Approval** | สร้างใบขออนุมัติ PE-F-0054-03 อัตโนมัติจาก Flowchart |
| **Save** | บันทึก Procedure ลง Browser (IndexedDB) |
| **Load** | โหลด Procedure ที่บันทึกไว้ |
| **Clear** | ล้าง Canvas ทั้งหมด |

### Canvas Navigation
| การกระทำ | ผล |
|----------|-----|
| **Scroll wheel** | Zoom in / out |
| **ลาก Canvas** | เลื่อนมุมมอง (Pan) |
| **ลาก Block** | ย้ายตำแหน่ง Block |
| **ปุ่ม 🔍 / Fit** | Zoom ให้พอดีหน้าจอ |

---

## 4. Block ทั้งหมด

### 🟢 Flow Control

| Block | ชื่อย่อ | หน้าที่ |
|-------|---------|---------|
| **START** | START | จุดเริ่มต้นของ Procedure (มีได้ 1 ตัว) |
| **END** | END | สิ้นสุด Procedure |
| **Branch** | BRANCH | แยกเส้นทางตามค่าตัวแปร (สูงสุด 10 case + else) |
| **Parallel (Split)** | PARALLEL | แยก Flow ออกเป็นหลายสายพร้อมกัน |
| **Parallel (Join)** | PARALLEL | รวม Flow กลับ — AND: รอทุกสาย / OR: รอสายใดสายหนึ่ง |
| **Input Connector** | IN-CONN | จุดรับ Flow จากที่อื่น |

### 🔵 Condition (เงื่อนไข)

| Block | ชื่อย่อ | หน้าที่ |
|-------|---------|---------|
| **AND / OR Gate** | AND/OR | ตรวจสอบเงื่อนไขหลายตัว — เลือกโหมด AND หรือ OR |
| **AND Gate** | AND | ทุกเงื่อนไขต้อง TRUE → YES, ไม่ใช่ → NO |
| **OR Gate** | OR | อย่างน้อย 1 เงื่อนไขต้อง TRUE → YES, ไม่ใช่ → NO |

**ตัวดำเนินการเงื่อนไขที่รองรับ:** `==` `!=` `>` `>=` `<` `<=`

**ตัวอย่าง:**
```
LC2404A.MV > 80   ← ค่า MV ของ tag ต้องมากกว่า 80
AND
LC2404A.PV >= 35  ← ค่า PV ต้องมากกว่าหรือเท่ากับ 35
```

### ⏱️ Timer & Clock

| Block | ชื่อย่อ | หน้าที่ |
|-------|---------|---------|
| **Timer (Seconds)** | TIMER | หน่วงเวลา N วินาที แล้วเดินต่อ |
| **Start Timer** | START TMR | เริ่มนับ Timer ที่กำหนด |
| **Stop Timer** | STOP TMR | หยุด Timer (ค่าที่นับคงอยู่) |
| **Pause Timer** | PAUSE TMR | หยุด Timer ชั่วคราว |
| **Restart Timer** | RESTART TMR | รีสตาร์ท Timer นับใหม่จากศูนย์ |
| **Check Elapsed Time** | CHK TIME | ตรวจว่า Timer ครบเวลาหรือยัง → YES / NO |

### 📡 Output to PCS

| Block | ชื่อย่อ | หน้าที่ |
|-------|---------|---------|
| **Output to PCS** | OUTPUT | ส่งค่าตัวเลขไปยัง DCS Tag (สูงสุด 5 tag/block) |
| **Block Mode** | MODE | เปลี่ยน Block Mode ของ DCS Tag: AUT / MAN / CAS / O / S |
| **Substitution** | SUBST | กำหนดค่าให้ Parameter/Variable (ไม่ใช่ DCS Tag โดยตรง) |

### 💬 Message

| Block | ชื่อย่อ | หน้าที่ |
|-------|---------|---------|
| **Confirmation** | CONFIRM | แสดง Popup รอ Operator กด OK ก่อนเดินต่อ |
| **Guidance Message** | GUIDE | แสดงข้อความแนะนำ แล้วเดินต่อทันที (ไม่ต้องยืนยัน) |
| **Alarm Message** | ALARM | แสดง Alarm สีแดง — Operator ต้อง Acknowledge ก่อน |

### 🔧 Utility

| Block | ชื่อย่อ | หน้าที่ |
|-------|---------|---------|
| **Calculation** | CALC | คำนวณนิพจน์ เช่น `sqrt(FC2405.PV * 100)` |
| **Sub Procedure** | SUBPROC | เรียก Sub-procedure ที่กำหนดไว้ |
| **Parameter** | PARAM | ประกาศ Parameter พร้อมค่าเริ่มต้น |

**ฟังก์ชันคำนวณที่รองรับ:** `sqrt`, `pow`, `abs`, `log`, `ln`, `exp`, `mod`, `round`, `ceil`, `floor`, `+`, `-`, `*`, `/`

---

## 5. การเชื่อมต่อเส้น (Edge)

### วิธีต่อเส้น
1. **Hover** ที่ Block จะเห็น Handle (จุดสี่เหลี่ยมเล็กๆ) รอบ Block
2. **ลาก** จาก Handle ต้นทาง → ปล่อยที่ Block ปลายทาง
3. เส้นจะถูกสร้างอัตโนมัติ

### ชนิดของเส้น

| ชนิด | สี | ความหมาย | ใช้กับ |
|------|----|-----------|--------|
| **Standard** | เทา | ทิศทางปกติ | ทุก Block |
| **YES** | เขียว 🟢 | เงื่อนไขผ่าน | AND/OR Gate |
| **NO** | แดง 🔴 | เงื่อนไขไม่ผ่าน | AND/OR Gate |
| **REP** | ส้มประ 🟠 | วนซ้ำ (Repetition loop) | Timer / AND/OR |

### เปลี่ยนชนิดเส้น
> **คลิกขวาที่เส้น** → เลือกชนิดที่ต้องการ:
> - Standard (ปกติ)
> - YES (เงื่อนไขผ่าน)
> - NO (เงื่อนไขไม่ผ่าน)
> - Repetition (วนซ้ำ)
> - ลบเส้นเชื่อม

### ปรับแนวเส้น
- **ลาก** ที่จุดสี่เหลี่ยมกลางเส้น เพื่อโค้งหรือเลี้ยวเส้นได้อิสระ

### ลบเส้น
- **คลิกขวา → ลบเส้นเชื่อม** หรือ
- **คลิกที่เส้น** แล้วยืนยัน

---

## 6. แท็บ Properties, Tags และ Coach

### 📋 Properties
คลิก Block บน Canvas → แท็บ Properties จะแสดง Config ของ Block นั้น เช่น:
- เงื่อนไข (Tag, Operator, Value) สำหรับ AND/OR Gate
- จำนวนวินาทีสำหรับ Timer
- DCS Tag และค่าที่จะส่งสำหรับ Output to PCS
- ข้อความสำหรับ Confirmation / Guidance / Alarm

### 📡 Tags
จัดการ **DCS Tag จำลอง** ที่ใช้ในการ Run:
- **เพิ่ม Tag** — กำหนดชื่อ, ชนิด (number/text), ค่าเริ่มต้น
- **แก้ไขค่า Tag** — เปลี่ยนค่าได้แม้ขณะ Run (จำลอง DCS real-time)
- **ลบ Tag** — ลบออกจากระบบจำลอง
- ขณะ Run จะแสดงค่า **real-time** ของทุก Tag

**Tag มาตรฐานที่มีให้ทดลองใช้:**
```
LC2404A.MV, LC2404A.PV, LC2404A.SV
FC2405.MV, FC2405.PV, FC2405.SV
PP404.MV, PP404.PV
```

### 🎯 Coach (Validator)
ตรวจสอบ Procedure **อัตโนมัติ** และแจ้งปัญหา:

| ระดับ | สัญลักษณ์ | ความหมาย |
|-------|-----------|-----------|
| **ERROR** | 🔴 | ต้องแก้ก่อน Run เช่น AND/OR ไม่มีเส้น YES |
| **WARNING** | 🟡 | ควรตรวจสอบ เช่น AND/OR ไม่มีเส้น NO |
| **OK** | 🟢 | ผ่านการตรวจสอบ พร้อม Run |

> คลิกที่รายการใน Coach เพื่อ **Jump ไปยัง Block ที่มีปัญหา** ทันที

---

## 7. Auto-Generate Wizard

กด **✦ Auto-Generate** ใน Toolbar เพื่อสร้าง Flowchart อัตโนมัติ:

1. **เลือก Template** หรือ **กำหนด Step เอง**
2. เพิ่ม Step ได้หลายประเภท:
   - ตรวจเงื่อนไข (AND/OR Check)
   - ส่งค่าไป DCS (Output to PCS)
   - รอ Timer
   - แสดงข้อความ (Guidance / Confirmation / Alarm)
3. กด **Generate** → Flowchart จะถูกสร้างบน Canvas อัตโนมัติ

---

## 8. การจำลองการทำงาน (Run)

### เริ่ม Run
1. ตรวจสอบ **Coach** → ต้องไม่มี ERROR
2. กด **▶ Run**
3. ดู Block ที่กำลังทำงาน (จะเป็นสีเขียวและกะพริบ)
4. ดู **Execution Console** ด้านล่างสำหรับ Log

### ปรับความเร็ว
เลือก Speed ใน Toolbar: `1x` `2x` `4x` `8x`

### สถานะของ Procedure
| สถานะ | ความหมาย |
|-------|-----------|
| **READY** | พร้อม Run |
| **RUNNING** | กำลังทำงาน |
| **PAUSED** | หยุดรอ Operator (Confirmation / Alarm) |
| **N ERR** | มี N Error ใน Coach |

### Popup ระหว่าง Run
- **Confirmation** → กด **ยืนยัน** เพื่อเดินต่อ
- **Guidance** → กด **OK** (เดินต่อทันที)
- **Alarm** → กด **รับทราบ** เพื่อ Acknowledge

### Execution Console
- แสดง Log ทุก Step แบบ Real-time
- ดู Tag ก่อน/หลังเปลี่ยนค่า
- ดูผล YES/NO ของเงื่อนไข
- กด **Clear** เพื่อล้าง Log

---

## 9. การบันทึกและโหลด Procedure

### บันทึก (Save)
- กด **Save** ใน Toolbar
- ข้อมูลถูกเก็บลง **IndexedDB ของ Browser** (ไม่หายเมื่อปิดแล้วเปิดใหม่)
- ไม่ต้องเชื่อมต่อ Internet

### โหลด (Load)
- กด **Load** เพื่อเรียก Procedure ที่บันทึกไว้

### ล้าง (Clear)
- กด **Clear** เพื่อล้าง Canvas ทั้งหมด (จะถามยืนยันก่อน)

> ⚠️ **หมายเหตุ:** ข้อมูลเก็บอยู่ใน Browser เท่านั้น หากต้องการแชร์ให้คนอื่น ให้ Copy โค้ดหรือ Export เป็นไฟล์

---

## 10. Approval Sheet (ใบขออนุมัติ)

ฟีเจอร์ **Approval Sheet** ช่วยสร้างใบขออนุมัติ **PE-F-0054-03** (GCM PTA) โดยดึงรายการขั้นตอนจาก Flowchart ที่ออกแบบไว้โดยอัตโนมัติ

### วิธีใช้งาน

1. **สร้าง Flowchart** ใน Canvas ให้สมบูรณ์ (ตั้งแต่ START ถึง END)
2. **กดปุ่ม `📋 Approval`** บน Toolbar (ขวามือ)
3. **กรอกข้อมูล** ในฟอร์ม
4. **กด `🖨 Print`** เพื่อพิมพ์ หรือ **`📋 Copy Plain Text`** เพื่อคัดลอก

### ฟิลด์ในฟอร์ม

| ฟิลด์ | รายละเอียด |
|-------|-----------|
| **Plant** | ชื่อหน่วยงาน / Plant (เช่น PTA#1, PTA#2) |
| **Topic** | ชื่อ Procedure — ดึงจากชื่อที่ตั้งบน Toolbar อัตโนมัติ |
| **Concept detail** | อธิบายวัตถุประสงค์และเหตุผลในการสร้าง Procedure นี้ |
| **ขั้นตอน (Step List)** | **ระบบดึงให้อัตโนมัติ** โดยเดิน Flowchart จาก START → END ตาม logic |
| **Create by B/M** | ชื่อผู้จัดทำ (Board Man) + วันที่ |
| **Check by F/M** | ชื่อผู้ตรวจ (Field Man) + วันที่ |
| **Approve by Sect. Mgr.** | ชื่อผู้อนุมัติระดับ Section + วันที่ |
| **Exapilot Num.** | หมายเลข Program ที่บันทึกใน Exapilot |
| **After program create finished** | เช็คบ็อกซ์: Sequence complete / Not relate with I/L |
| **Test by F/O / B/M / F/M** | ผู้ทดสอบในแต่ละระดับ + วันที่ |
| **Approve for start apply** | ผู้อนุมัติให้เริ่มใช้งานจริง + วันที่ |
| **Acknowledgement** | ตารางลงชื่อรับทราบ Shift A/B/C/D (F/O1, F/O2, B/M, F/M) |

### รายการขั้นตอนอัตโนมัติ (Auto Step List)

ระบบจะเดิน Flowchart ตั้งแต่ START ตาม logic จริง:
- เลือกเส้น **YES** → **out (standard)** → non-NO/non-REP ตามลำดับ
- หยุดที่ **END** หรือเมื่อครบ 100 steps
- แต่ละ Block แสดงเป็นรายการที่อ่านง่าย เช่น:
  ```
  1. [START] เริ่มต้น Procedure
  2. [CONFIRM] Confirm ว่า Start PP-404A
  3. [AND GATE] ตรวจสอบ: LC2404A.MV > 80 AND LC2404A.PV >= 35
     └─ ไม่ผ่าน → วนซ้ำ รอ 5 วิแล้วตรวจซ้ำ
  4. [OUTPUT] ส่งค่า PCS: LC2404A.MV=0
  5. [END] สิ้นสุด Procedure
  ```

### ปุ่มในฟอร์ม

| ปุ่ม | หน้าที่ |
|------|---------|
| **🖨 Print** | เปิดหน้าต่างพิมพ์ A4 แนวตั้ง — พร้อม Logo GCM PTA และ `PE-F-0054-03` มุมขวาล่าง |
| **📋 Copy Plain Text** | คัดลอกรายการขั้นตอนเป็น Plain Text สำหรับนำไปใช้ใน Email / เอกสาร |
| **✕ Close** | ปิดฟอร์ม (ข้อมูลที่กรอกจะหายเมื่อปิด) |

> 💡 **เคล็ดลับ:** กรอก **Concept detail** ให้ชัดเจน เช่น "Wash PP-404A เพื่อเตรียม Start-up หลังจาก Maintenance" เพื่อให้หัวหน้าเข้าใจวัตถุประสงค์ก่อนดูรายการขั้นตอน

---

## 11. Keyboard Shortcuts

| คีย์ | หน้าที่ |
|------|---------|
| `Delete` / `Backspace` | ลบ Block ที่เลือก |
| `Escape` | ยกเลิกการลากเส้น / ยกเลิกการเลือก |
| `Scroll Wheel` | Zoom in / out บน Canvas |

---

## 12. เคล็ดลับการใช้งาน

### ✅ Best Practices

1. **ตรวจ Coach ก่อน Run เสมอ** — AND/OR Gate ต้องมีเส้น YES เสมอ ส่วนเส้น NO ควรมีเพื่อจัดการกรณีเงื่อนไขไม่ผ่าน

2. **Pattern วนซ้ำ (Loop)** — ใช้ Timer + REP edge วนกลับไป AND/OR Gate เพื่อรอเงื่อนไข:
   ```
   AND/OR Gate --[NO]--> Timer (รอ 5 วินาที) --[REP]--> AND/OR Gate
   AND/OR Gate --[YES]--> ขั้นตอนต่อไป
   ```

3. **ตั้งชื่อ Tag ให้ถูกรูปแบบ** — ใช้ `TAGNAME.FIELD` เช่น `FC2405.PV`, `LC2404A.MV`

4. **ใช้ Guidance** สำหรับข้อความแนะนำ Operator ที่ไม่ต้องการหยุดรอ และ **Confirmation** เมื่อต้องการให้ Operator ยืนยันก่อนเดินต่อ

5. **ปรับแนวเส้น** — ลากจุดกลางเส้นเพื่อจัดเส้นให้ไม่ทับกัน อ่านง่ายขึ้น

6. **เปลี่ยนชนิดเส้น** — คลิกขวาที่เส้นแล้วเลือก YES / NO / REP / Standard ได้ตลอดเวลา

7. **ทดลอง Auto-Generate** ก่อน แล้วค่อยแก้ไข Detail — ประหยัดเวลากว่าสร้างจากศูนย์

---

## สีของ Block

| สี | หมวด |
|----|------|
| 🟢 เขียว pill | START |
| 🔴 แดง pill | END |
| 🔵 น้ำเงิน | AND / OR Gate (condition) |
| 🟦 น้ำเงินเข้ม | AND Gate |
| 🟣 ม่วง | OR Gate |
| ⬜ ขาว แถบสีตาม cat | Output, Timer, Message, Utility |

---

## เกี่ยวกับ

- **Version:** 3.0
- **ผู้พัฒนา:** Supasit A
- **Repository:** [https://github.com/supasiao7896TH/Exapilot-Studio](https://github.com/supasiao7896TH/Exapilot-Studio)
- **License:** MIT
