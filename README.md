# image-craft-lv

> สกิล Claude Code ที่เรียนรู้ได้เอง สำหรับ **ยกระดับ prompt engineering ภาพนิ่ง** (Nano Banana, Midjourney, DALL·E, Stable Diffusion, Flux ฯลฯ)

ทุกครั้งที่เขียน prompt สร้างภาพ สกิลจะบังคับให้ผ่าน **Pre-submit Checklist + Batch Gate** ก่อน submit และรัน **Post-generate Self-review** ก่อนส่งให้ผู้ใช้ — พร้อมเก็บ **บทเรียน (lessons)** ที่เลเวลอัปได้จริงเมื่อได้รับการ validate ข้ามโปรเจกต์

สกิลมี 3 ระบบทำงานร่วมกัน: **Lessons Library** (บทเรียนที่สะสมจากการใช้งานจริง) + **Leveling System** (บทเรียนต้องผ่าน validation ข้ามหลายโปรเจกต์ถึงจะเลเวลอัป) + **Arena** (ระบบทดสอบสังเคราะห์ด้วย AI 4 ตัว ที่ validate บทเรียนได้แม้ไม่มีโปรเจกต์ใหม่เข้ามา)

📊 **[เปิดบอร์ดสรุปภาพรวม (ภาษาไทย)](lessons-board.html)** — 12 บทเรียน · เส้นทางวิวัฒนาการ · หลักการ · arena system

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

Claude ควรเรียก `image-craft-lv` ขึ้นมาอัตโนมัติ และเริ่มจาก ENTRY PROTOCOL ก่อน

---

## หัวใจของสกิล

### 🎯 THE RULE

> ก่อน submit prompt ภาพใดๆ → รัน **Batch Gate** + **Pre-submit Checklist**
> ก่อนส่งผลลัพธ์ให้ผู้ใช้ → รัน **Post-generate Self-review**
> ไม่มีข้อยกเว้น ข้าม = LV regression

### 📋 Pre-submit Checklist (14 ข้อ)

แบ่ง 4 กลุ่ม ที่ Claude จะแปลงเป็น TodoWrite อัตโนมัติทุก session:

| กลุ่ม | ประเด็น |
|------|---------|
| A. Consistency audit | ตัวละคร / สถานที่ / prop ซ้ำ มี ref หรือ master anchor หรือยัง? Design-language ตรงไหม? |
| B. Ambiguity sweep | Orientation ของ subject ซ่อน/บางส่วน, ตัวเลข > adjectives, ชื่อ lens/angle, negative prompts, distinguishable characters |
| C. Reference strategy | Ref เหมาะสมไหม? อยู่ใต้ limit ของโมเดล? Chain order ถูกต้อง? |
| D. Phase planning | วาด dependency graph, parallel ใน phase / sequential ระหว่าง phase |

### 🔍 Post-generate Self-review (7 ข้อ)

1. Anatomical plausibility (ใช้ตัวเลข ห้าม eyeball)
2. Orientation
3. Design-language drift cross-shot
4. Within-image consistency (แสง/เงา)
5. Intent fulfillment (re-read prompt เทียบภาพ)
6. 🔴 **Proportion comparison ใช้ ORIGINAL ref ไม่ใช่ crop**
7. 🔴 **Full-frame scan หลัง regen — อย่า tunnel-vision**

---

## ระบบ Leveling

### ปัจจุบัน: **LV 2.4** (first lesson validated + Arena operational)

**สถานะบทเรียน:** 1 validated (L09) · 11 pending · 0 retired

ดูประวัติทั้งหมด → [CHANGELOG.md](CHANGELOG.md)

### บทเรียนเลเวลอัปได้ยังไง

ทุกบทเรียน (lesson) เริ่มต้นเป็น `pending (X/Y)` ต้องผ่าน **Validation Gate** เพื่อเลื่อนเป็น `validated`:

| Tier | ความหมาย | จำนวน pass | โปรเจกต์ที่ต้องใช้ |
|------|----------|-----------|---------------------|
| **Micro** | เปลี่ยน phrasing/naming เล็กๆ | 1/1 | 1 project |
| **Meso** | เทคนิคระดับ per-shot | 2/3 | **≥2 projects** |
| **Macro** | เปลี่ยน workflow ทั้งระบบ | 3/5 | **≥3 projects** (หรือ 3 pass + 1 counter-test) |

**กฎ cross-project** (ใหม่ใน LV 2.1): ป้องกัน lesson ที่ validate บนโปรเจกต์เดียวแล้วอ้างว่า portable — ของที่ portable จริงต้องผ่านข้ามโปรเจกต์

### จังหวะ log

ทุกครั้งที่ใช้ lesson กับงานจริง → เพิ่ม row ใน [VALIDATION_LEDGER.md](VALIDATION_LEDGER.md) + mirror ลง Validation log ของ lesson นั้น — เมื่อถึง threshold → promote + bump LV

---

## 🏟️ Arena — ระบบทดสอบสังเคราะห์

ปัญหาที่ระบบ Leveling เจอคือ: ถ้าเราไม่ได้ทำโปรเจกต์จริงบ่อยๆ บทเรียนก็ไม่เคยได้ข้าม cross-project validation — ค้างอยู่ใน `pending` ตลอด

**Arena** (เพิ่มใน LV 2.2) คือระบบที่ให้ **AI 4 ตัวแบ่งบทบาทและเล่นกันเอง** เพื่อจำลอง "โปรเจกต์สังเคราะห์" ที่ใช้ validate บทเรียนได้จริง

### 4 AI roles

| Role | หน้าที่ |
|------|---------|
| 🎲 **Generator** | สร้าง scenario ใหม่ที่ต่างจากโปรเจกต์เดิม ≥3 แกน (จาก 9 แกน) + เขียน pass criteria ล็อคไว้ก่อน |
| 🖌️ **Runner (blinded)** | ทำงานตาม scenario โดยไม่รู้ว่ากำลังทดสอบ lesson ไหน · เรียก API สร้างภาพจริง |
| ⚖️ **Judge** | ให้คะแนนตาม criteria ที่ล็อคไว้ · ห้ามแก้ criteria ย้อนหลัง |
| 🕵️ **Skeptic** | ตั้งคำถาม "test ยากพอไหม / lesson จำเป็นจริงไหม" — void trial ได้แม้ Judge ให้ pass |

### หลักการป้องกัน Goodhart's law

- **9-axis diversity** — ทุก scenario ต้อง flip ≥3 axes จาก DHYANA + ≥2 axes จาก scenarios ก่อนหน้า
- **Pre-registered criteria** — เกณฑ์ล็อคก่อน Runner เริ่ม ห้ามเปลี่ยนภายหลัง
- **Blinded Runner** — ป้องกัน bias เพราะรู้ว่ากำลังโดนทดสอบเทคนิคอะไร
- **Skeptic gate** — ถ้า scenario ออกแบบง่ายเกิน → void ทั้งที่ Judge ให้ pass

### ผลลัพธ์ที่รันไปแล้ว (4 trials)

| Trial | Scenario | ผล |
|-------|----------|-----|
| S01 | 1920s general store | **void** — text over-specified, ไม่ isolate lesson ได้ |
| S02 | Feudal Japan tsuba (A/B control) | **partial** — 3A ชนะ 3B 2/4 dims |
| S03 | Ancient Aztec penacho | **PASS** — 3A ชนะ 3/4 dims → **triggered L09 promotion** |
| S04 | Victorian orrery (multi-factor) | **findings** — พบ blindspot ของ L09 → สร้าง L12 (dual-ref) |

**ต้นทุน API รวม 4 trials:** ~$1.17

ดูรายละเอียด → [`arena/README.md`](arena/README.md) · [`arena/axes.md`](arena/axes.md) · [`arena/scenario-bank/README.md`](arena/scenario-bank/README.md)

---

## โครงสร้างโฟลเดอร์

```
image-craft-lv/
├── SKILL.md                     # Engine — ส่วนที่ Claude โหลดทุก session
├── CHANGELOG.md                 # ประวัติ LV + Leveling Protocol
├── VALIDATION_LEDGER.md         # Append-only ledger (log งานที่ใช้ lesson จริง)
├── README.md                    # ไฟล์ที่คุณกำลังอ่านอยู่
├── lessons-board.html           # บอร์ดสรุปภาพรวม (ภาษาไทย)
│
├── lessons/                     # 12 บทเรียน จัดกลุ่ม 7 theme
│   ├── README.md                # Index ทุก lesson
│   ├── consistency/   (3)       # L01, L03, L08
│   ├── references/    (4)       # L05, L09 ✓, L11, L12
│   ├── orientation/   (1)       # L02
│   ├── character/     (1)       # L06
│   ├── delivery/      (1)       # L07
│   ├── workflow/      (1)       # L04
│   └── model-limits/  (1)       # L10
│
├── templates/
│   ├── session-kickoff.md       # 5-step intro ที่ Claude รันต้น session
│   ├── lesson-template.md       # Skeleton สำหรับเขียน lesson ใหม่
│   └── batch-plan-template.md   # Dependency-graph planner สำหรับโปรเจกต์ multi-shot
│
└── arena/                       # ระบบทดสอบสังเคราะห์ (LV 2.2+)
    ├── README.md                # คู่มือ operator
    ├── axes.md                  # 9-axis diversity rules
    ├── run-playbook.md          # 8-step workflow สำหรับรัน trial
    ├── scenario-bank/           # Index scenario ทั้งหมด + anti-reuse
    ├── criteria/                # Criteria template ต่อ lesson (11 files)
    ├── prompts/                 # 4 AI role prompts
    ├── trial-records/           # Archive ทุก trial (S01-S04 แล้ว)
    └── void-log.md              # Trial ที่ void (ไม่นับ ledger)
```

---

## Lessons ปัจจุบัน (12 อัน · 1 validated · 11 pending)

| ID | Theme | Status | หัวข้อ |
|----|-------|--------|--------|
| [L01](lessons/consistency/L01-ref-chains.md) | consistency | pending 1/5 · macro | Reference chains beat text-only for multi-shot sets |
| [L02](lessons/orientation/L02-face-orientation.md) | orientation | pending 1/3 · meso | Face orientation inside containers must be explicit |
| [L03](lessons/consistency/L03-opaque-transparent.md) | consistency | pending 1/3 · meso | Opaque vs transparent surfaces must match across set |
| [L04](lessons/workflow/L04-self-review-protocol.md) | workflow | pending 0/5 · macro | Self-review before showing output |
| [L05](lessons/references/L05-back-view-refs.md) | references | pending 0/3 · meso | Back-view refs cannot lock face identity |
| [L06](lessons/character/L06-distinguishable-characters.md) | character | pending 1/3 · meso | Distinguish lookalike characters with immutable features |
| [L07](lessons/delivery/L07-reviewable-artifacts.md) | delivery | pending 1/5 · macro | Deliverables as reviewable artifacts |
| [L08](lessons/consistency/L08-palette-consistency.md) | consistency | pending 1/3 · meso | Palette consistency within same world/time |
| [L09](lessons/references/L09-crop-refs.md) | references | **✅ validated 2.5/3 · meso** | Crop refs to isolate target element |
| [L10](lessons/model-limits/L10-prominence-floor.md) | model-limits | pending 1/5 · macro | Recognize prominence floor; stop diminishing-return regens |
| [L11](lessons/references/L11-video-continuity-refs.md) | references | pending 0/5 · macro | Tier-1 refs designed for video-pipeline continuity |
| [L12](lessons/references/L12-dual-ref.md) | references | pending 0/3 · meso | Dual-ref (crop + full scene) when target + background both matter |

**L09 เป็นบทเรียนแรกที่ผ่าน validation** — ผ่าน 3 projects (DHYANA + arena:S02 partial + arena:S03 pass) · **L12 เพิ่งเกิดจาก blindspot ที่พบใน S04** (ครอปอย่างเดียวทำให้ bg drift เมื่อช็อตกว้างกว่าครอป)

บทเรียนอื่นยัง `pending` — ต้องการ project ที่ 2/3 (จริงหรือ arena) เพื่อให้ผ่าน cross-project validation

---

## เขียน lesson ใหม่ยังไง

1. Copy [`templates/lesson-template.md`](templates/lesson-template.md)
2. วางใน `lessons/<theme>/L##-short-title.md`
3. กรอก frontmatter (id, theme, tier, status=pending, validation=0/Y, tags, origin_project, created)
4. เขียน body: TL;DR, Context, Mistake, Why it happened, Fix, Broader rule, Validation log, Cross-references
5. เมื่อใช้งานกับโปรเจกต์จริง → เพิ่ม row ใน `VALIDATION_LEDGER.md` และ mirror ใน lesson's Validation log
6. ครบ threshold + cross-project → promote ใน `CHANGELOG.md` + bump LV + commit

---

## Sister skills

- **[seedance-craft-lv](https://github.com/trin-zenityx/seedance-craft-lv)** — โครงเดียวกัน สำหรับ video generation ผ่าน ByteDance Seedance (มี Cost-Discipline Gate, 3 modes ของ Seedance 2.0)
- **`kie-nano-banana`** — layer สำหรับเรียก KIE.ai API โดยตรง (execution layer; สกิลนี้เป็น strategy layer เหนือมัน)

---

## Rollback

ถ้าสกิลทำงานผิดหลัง update ใด update หนึ่ง:

```bash
cd ~/.claude/skills/image-craft-lv
git log SKILL.md              # ดูประวัติ
git revert <sha>              # ย้อน commit ที่พลาด (keeps history)
```

กรณี rollback สุดขั้ว กลับไป LV 2 ก่อน redesign:
```bash
git reset --hard pre-redesign-lv2
```

---

## ปรัชญา

สกิลนี้ตั้งอยู่บน 6 Core Principles ที่ไม่เปลี่ยนระหว่าง LV:

1. **Mismatch between shots beats beauty per shot** — ภาพสอง shot ที่ match กันพอใช้ ดีกว่าสอง shot สวยมากแต่ไม่ match
2. **Ambiguity = model's choice, not yours** — ทุกรายละเอียดที่ไม่ได้บอก โมเดลตัดสินให้
3. **Reference images = foundational** — ไม่ใช่ optional polish; design chain ก่อน generate ครั้งแรกเสมอ
4. **Numbers > adjectives** — "2.1 เมตร" ไม่ใช่ "ยาว"; "85mm" ไม่ใช่ "telephoto"
5. **Negative-state common failures** — "no age markers, no text, no watermark, no [failure mode ที่เคยเจอ]"
6. **Self-review ไม่ใช่ optional** — เป็นขั้นสุดท้ายของ generation

---

## License

ส่วนตัวใช้ได้อิสระ ถ้านำไปใช้ต่อ/พัฒนาต่อขอ credit กลับมา 🙏

**Author:** [@trin-zenityx](https://github.com/trin-zenityx)
