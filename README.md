# image-craft-lv

> สกิล Claude Code ที่เรียนรู้ได้เอง สำหรับ **ยกระดับ prompt engineering ภาพนิ่ง** (Nano Banana, Midjourney, DALL·E, Stable Diffusion, Flux ฯลฯ)

ทุกครั้งที่เขียน prompt สร้างภาพ สกิลจะบังคับให้ผ่าน **Pre-submit Checklist + Batch Gate** ก่อน submit และรัน **Post-generate Self-review** ก่อนส่งให้ผู้ใช้ — พร้อมเก็บ **บทเรียน (lessons)** ที่สะสมจากการใช้งานจริง

สกิลคู่กัน — [`seedance-craft-lv`](https://github.com/trin-zenityx/seedance-craft-lv) สำหรับวิดีโอ

---

## Quick start

### ติดตั้ง

```bash
cd ~/.claude/skills/
git clone https://github.com/trin-zenityx/image-craft-lv.git
```

หลัง clone ครั้งเดียว Claude Code จะตรวจเจอ skill อัตโนมัติเมื่อคุณสั่งสร้าง/เขียน prompt ภาพนิ่ง

### ทดสอบว่า skill โผล่

เปิด Claude Code session ใหม่แล้วลองพิมพ์:

```
write a Nano Banana prompt for a rainy tokyo alley
```

Claude ควรเรียก `image-craft-lv` ขึ้นมาอัตโนมัติ

---

## หัวใจของสกิล

### 🎯 THE RULE

> ก่อน submit prompt ภาพใดๆ → รัน **Batch Gate** + **Pre-submit Checklist**
> ก่อนส่งผลลัพธ์ให้ผู้ใช้ → รัน **Post-generate Self-review**

### 📋 Pre-submit Checklist

แบ่ง 4 กลุ่ม:

| กลุ่ม | ประเด็น |
|------|---------|
| A. Consistency audit | ตัวละคร / สถานที่ / prop ซ้ำ มี ref หรือ master anchor หรือยัง? Design-language ตรงไหม? |
| B. Ambiguity sweep | Orientation ของ subject ซ่อน/บางส่วน, ตัวเลข > adjectives, ชื่อ lens/angle, negative prompts, distinguishable characters |
| C. Reference strategy | Ref เหมาะสมไหม? อยู่ใต้ limit ของโมเดล? Chain order ถูกต้อง? |
| D. Phase planning | วาด dependency graph, parallel ใน phase / sequential ระหว่าง phase |

### 🔍 Post-generate Self-review

1. Anatomical plausibility (ใช้ตัวเลข ห้าม eyeball)
2. Orientation
3. Design-language drift cross-shot
4. Within-image consistency (แสง/เงา)
5. Intent fulfillment (re-read prompt เทียบภาพ)
6. 🔴 **Proportion comparison ใช้ ORIGINAL ref ไม่ใช่ crop**
7. 🔴 **Full-frame scan หลัง regen — อย่า tunnel-vision**

---

## ระบบ Leveling (แบบ simple)

ปัจจุบัน: **LV 2.12** · 27 active lessons · 1 archived

ดูประวัติทั้งหมด → [CHANGELOG.md](CHANGELOG.md)

### บทเรียนเพิ่มยังไง

1. Claude สังเกต pattern / mistake / insight ที่น่าเก็บ → **เสนอ lesson + เหตุผล**
2. คุณตอบ: **yes** (เพิ่มเข้า library), **edit** (แก้แล้วเพิ่ม), **no** (ไม่เอา)
3. ถ้า yes — Claude copy `templates/lesson-template.md` ไปวางในธีมที่ตรง + อัปเดต `lessons/README.md`

### LV ขึ้นยังไง

1. เมื่อ active lessons สะสมพอที่จะ "เปลี่ยน behavior อย่างมีนัยสำคัญ" → Claude **เสนอ LV bump + เหตุผล**
2. คุณตอบ: **yes / no / wait**
3. ถ้า yes — Claude bump `level:` ใน frontmatter + เพิ่มเอนทรีใน `CHANGELOG.md`

Patch / minor / major เป็น judgment call:
- **Patch** — 1 lesson เพิ่ม/refine
- **Minor** — หลาย lessons หรือเปลี่ยน checklist/workflow
- **Major** — เปลี่ยน model family หรือโครงสร้าง

### Archive

บทเรียนที่ไม่เกี่ยวแล้ว (model เปลี่ยน, ถูก lesson ใหม่แทนที่, พิสูจน์ว่าผิด) → ย้ายไป `lessons/archive/` พร้อมโน้ตเหตุผลใน `lessons/README.md`

---

## โครงสร้างโฟลเดอร์

```
image-craft-lv/
├── SKILL.md                 # Engine — Claude โหลดทุก session
├── CHANGELOG.md             # ประวัติ LV
├── OUTCOMES_HISTORY.md      # Audit log ของการใช้ lesson จริง
├── README.md                # ไฟล์ที่คุณกำลังอ่าน
│
├── lessons/                 # 27 active lessons + archive (L15)
│   ├── README.md            # Index + retrieval cheatsheet
│   ├── consistency/   (3)
│   ├── references/    (4)
│   ├── orientation/   (1)
│   ├── character/     (4)
│   ├── delivery/      (2)
│   ├── workflow/      (4)
│   ├── model-limits/  (1)
│   ├── filter/        (2)
│   ├── pose/          (2)
│   ├── camera/        (1)
│   ├── aesthetic/     (1)
│   ├── prompt-craft/  (2)
│   └── archive/       (1)   # L15 (retired)
│
└── templates/
    ├── lesson-template.md       # Skeleton สำหรับ lesson ใหม่
    └── batch-plan-template.md   # Dependency-graph planner
```

---

## Sister skills

- **[seedance-craft-lv](https://github.com/trin-zenityx/seedance-craft-lv)** — โครงเดียวกัน สำหรับ video generation ผ่าน ByteDance Seedance
- **`kie-nano-banana`** — layer สำหรับเรียก KIE.ai API โดยตรง (execution layer; สกิลนี้เป็น strategy layer เหนือมัน)
- **`internal-board-builder`** — local HTML review boards (L16's home)

---

## Rollback

ถ้าสกิลทำงานผิดหลัง update ใด:

```bash
cd ~/.claude/skills/image-craft-lv
git log SKILL.md              # ดูประวัติ
git revert <sha>              # ย้อน commit ที่พลาด
```

---

## ปรัชญา

สกิลนี้ตั้งอยู่บน Core Principles ที่ไม่เปลี่ยนระหว่าง LV (ดูใน [SKILL.md](SKILL.md)):

1. **Mismatch between shots beats beauty per shot** — ภาพสอง shot ที่ match กันพอใช้ ดีกว่าสอง shot สวยมากแต่ไม่ match
2. **Ambiguity = model's choice, not yours** — ทุกรายละเอียดที่ไม่ได้บอก โมเดลตัดสินให้
3. **Reference images = foundational** — ไม่ใช่ optional polish; design chain ก่อน generate ครั้งแรกเสมอ
4. **Numbers > adjectives** — "2.1 เมตร" ไม่ใช่ "ยาว"; "85mm" ไม่ใช่ "telephoto"
5. **Negative-state common failures** — "no age markers, no text, no watermark, no [failure mode ที่เคยเจอ]"
6. **Self-review ไม่ใช่ optional** — เป็นขั้นสุดท้ายของ generation
7. **Face identity is HIGHER priority than pose / action fidelity**
8. **Filter problems** = layer × tier diagnosis → ใช้สกิล **`filter-craft-lv`** (ย้ายจาก L13/L17/L18)

---

## License

ส่วนตัวใช้ได้อิสระ ถ้านำไปใช้ต่อ/พัฒนาต่อขอ credit กลับมา 🙏

**Author:** [@trin-zenityx](https://github.com/trin-zenityx)
