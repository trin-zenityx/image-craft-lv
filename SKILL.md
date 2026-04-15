---
name: prompt-craft-lv
description: Self-improving image and video prompt engineering with level tracking and mandatory pre-submit checklist. Use whenever about to write or submit a prompt for image/video generation (Nano Banana, Seedance, Midjourney, etc.) — especially in multi-shot or multi-image projects where character/location/style consistency matters. Auto-invoke before any generation request.
level: 2
updated: 2026-04-15
---

# Prompt Craft LV

> A living skill. Every time I learn from a mistake or a validated success, I level up and log the lesson here. Future-me reads this before writing any prompt.

## Current Level: **LV 2**

### Level Changelog

- **LV 1** (baseline) — Text-only prompting. Relied on repeating prose descriptions to maintain consistency across multi-image sets. Trusted the model to interpret prose faithfully.
- **LV 2** (2026-04-15) — Learned: reference chains, explicit orientation control, design-language consistency, mandatory self-review before delivery.

---

## THE RULE (non-negotiable)

**Before submitting ANY image or video generation prompt, run the Pre-submit Checklist below. Before showing generated output to the user, run the Post-generate Self-review. No exceptions.**

Skipping = LV regression.

---

## PRE-SUBMIT CHECKLIST

Run this mentally (or as visible TODO) before every generate call:

### A. Consistency audit
- [ ] **Recurring character?** If yes, is there a reference image attached (`--reference` / `@image_n`)? If no ref exists yet, are you generating the master anchor FIRST before any derivative shot?
- [ ] **Recurring location?** Same question — master anchor first, then refs.
- [ ] **Recurring prop/motif?** (e.g., a specific butterfly, pod, weapon)
- [ ] **Design-language match?** If the ref shows OPAQUE containers, new shot says OPAQUE. If ref shows RED accent, new shot says RED. Never let the model "re-decide" established visual facts.

### B. Ambiguity sweep
- [ ] **Orientation of hidden/partial subjects?** Faces inside windows/containers/mirrors — state direction explicitly ("face upward to ceiling", "body facing away from camera"). Models default to "face the visible camera/window" (human-logic) which is often wrong for your intent.
- [ ] **Dimensions stated?** "Human-length pod (2.1 m)" reads differently than "pod". Numbers > adjectives.
- [ ] **Camera angle & lens named?** Not "a shot of X" but "telephoto 85mm low-angle 3/4 view".
- [ ] **Negative prompts for common drift?** "No text, no watermark, no age-markers, no [specific common failure]"
- [ ] **Character distinguishability?** If two DIFFERENT characters appear in similar contexts (e.g., two different people both sleeping in pods), have you specified visibly different immutable features (gender, ethnicity, hair color/length, facial structure)? Otherwise model renders both as "generic X" and viewers can't tell them apart, destroying plot beats.

### C. Reference strategy
- [ ] **Refs chosen are the MOST relevant?** Not just any Tier 1 image — specifically the ones locking the visual elements in this shot.
- [ ] **Under the model's ref limit?** (Nano Banana Pro: 8, Nano Banana 2: 14, Seedance Omni: 9.)
- [ ] **Chain order?** If building a set, generate master anchors first, then secondary (ref masters), then tertiary (ref masters + secondary).

### D. Phase planning (multi-image projects)
- [ ] **Drawn the dependency graph?** Which images depend on which as refs?
- [ ] **Parallel within phase, sequential between phases?** Don't wait for whole set to complete when a phase can go parallel.

---

## POST-GENERATE SELF-REVIEW

Before showing output to user, scan each image for:

1. **Anatomical plausibility** — pod proportions, body in pose, scale of figure vs environment. If a 2m pod looks like a 60cm capsule, flag it. **Quantify ratios, don't eyeball.** Estimate percentages: "face window is X% of pod length, face fills Y% of window".
2. **Orientation** — does the face point where you intended? Hand pose match ref?
3. **Design-language drift** — does the opaque-body pod in shot A still look opaque in shot B of the same set? Did the character's robe change color?
4. **Within-image internal consistency** — is the light direction consistent with the shadows? If a window is to the left, is the rim light coming from the left?
5. **Intent fulfillment** — reread your own prompt's key phrases. Does the image show "weathered hands with cyan rim"? Or just generic hands?

**CRITICAL — Proportion comparison rule:** When checking "does X match ref Y" for proportions, compare to the **ORIGINAL full-scale ref image**, NOT a zoomed/cropped version. A crop enlarges the target in your field of view, which tricks you into thinking the proportions in the new image are fine when they may be 2-3x too large. Do the comparison at equal zoom levels.

**If anything fails: regenerate with a fix, don't ship the broken version hoping user won't notice.**

---

## LESSONS LIBRARY

Concrete mistakes + fixes. Grows over time. Always include: **Tier, Status, Context, Mistake, Why, Fix, Validation log.**

---

### L1 — Reference chains beat text-only for multi-shot sets
**Tier:** Macro (workflow-level)
**Status:** `pending (1/5)` — validated once on DHYANA Tier 1 v2; needs 2 more successes on unrelated projects
**Context:** DHYANA project Tier 1 round 1 — 12 anchor images for a 25-shot short film.
**Mistake:** Generated all 12 with text-only prompts. Relied on verbal repetition ("saffron robe, shaved scalp, weathered olive-tan skin") to keep Tenzin's face consistent across #1 frontal and #2 profile.
**Why it happened:** Assumed prose repetition was sufficient. Didn't think about model's stochastic interpretation per call.
**Result:** Face drifted — #1 Tenzin and #2 Tenzin were clearly different people. Cathedral in #5 and pod corridor in #6 had different architectural language.
**Fix:** Build dependency graph. Generate master anchors first (no refs). Generate secondary with master refs. Generate tertiary with master + secondary refs. Per the Nano Banana skill, pass `--reference path/to/anchor.png` as many times as needed.
**Applied:** Tier 1 v2 (all 12 regenerated). Face locked. Architecture locked. Pod design locked.

### L2 — Face orientation inside containers must be explicit
**Tier:** Meso (per-shot discipline)
**Status:** `pending (1/3)` — validated once on DHYANA #7 v5; needs 2 more successes
**Context:** DHYANA #7 pod detail — full-body pod, sleeping face visible through face-window.
**Mistake:** Wrote "the calm sleeping face of an adult human, visible through the frosted face-window". Did not specify which way the face was oriented.
**Why it happened:** Human logic says "if face is visible through window, face is probably turned to window" — but that's the model's assumption, not your intent. Your intent was "supine body, face up to ceiling, visible through top-mounted porthole".
**Result:** Multiple versions of #7 came back with face turned sideways toward the glass, looking awkward and inconsistent with #6 where other pod faces were oriented up.
**Fix:** Always state face direction explicitly: "face turned UPWARD to the ceiling, body supine, face visible through the window from above" or "face turned forward to camera at three-quarters" — never leave it unstated.
**Broader rule:** Any time a face/body is seen through a window/mirror/transparent surface, specify (a) subject orientation, (b) camera position relative to subject, (c) what viewer sees through the glass.
**Applied:** #7 v5 (pending at time of logging).

### L3 — Opaque vs transparent container surfaces must match across the set
**Tier:** Meso (per-shot discipline with cross-shot consequence)
**Status:** `pending (1/3)` — validated once on DHYANA #7 v4; needs 2 more
**Context:** DHYANA pods — #6 corridor and #7 detail.
**Mistake:** Said "transparent/frosted panels" in the detail prompt, same subject but different word choice than corridor prompt. Model rendered #6 with entirely opaque bodies (only face-window) and #7 with transparent-torso panels.
**Why it happened:** Vague wording + no cross-shot design-language statement. Each prompt re-decides the design.
**Fix:** In any multi-shot prompt set, pick one unambiguous phrase for each surface treatment and use it identically: "completely OPAQUE white ceramic shell along entire body, with face-window as the only transparent surface". Then mirror it exactly in every prompt that features that object.
**Applied:** #7 v4 (opaque body, face-window only) — matched #6.

### L9 — Crop reference images to isolate the target element; full-scene refs introduce noise
**Tier:** Meso (technique with broad reuse)
**Status:** `pending (1/3)` — validated once on DHYANA #07 v7; needs 2 more
**Context:** DHYANA #07 pod detail — multiple regen attempts (v3, v4, v5, v6) all used the full pod corridor image (#06) as reference. Each regen produced pods with different shapes — a bulgy egg, a compact head-only capsule, a disproportioned hybrid — none matched the sleek elongated capsule shape visible in #06.
**Mistake:** Passed the entire corridor image as ref when only ONE specific object needed to be matched exactly. The model had too much visual information (corridor, water, multiple pods at various angles, background racks) and couldn't decide which element was the "target". It reinterpreted pod shape each generation.
**Why it happened:** Treated "use reference" as "pass the related image". Did not consider that the ref's job is to anchor a specific visual element, and including unrelated elements dilutes that anchor.
**Result:** Four failed regens before realizing the problem. User had to point out that the pod looked different each time.
**Fix:** When a ref needs to lock ONE element (specific object, specific pose, specific color), crop the source image to contain ONLY that element. Use PIL/ImageMagick to extract the tight region. Pass the crop as the primary ref. This gives the model an unambiguous visual target.
**Broader rule:** A reference image teaches the model what it shows, in proportion to how much of the frame that thing occupies. If the pod is 10% of a scene ref, the pod design is 10% "loud" to the model. If the pod fills the frame of a cropped ref, it is 100% loud.
**Applied:** #07 v7 generated using a cropped front pod from #06 (1885x1280 crop of 4096x2286 original) — pod silhouette finally matched the corridor reference exactly.
**Related technique — Nano Banana Pro edit mode:** Per research, Nano Banana Pro treats reference images with edit-style prompting ("match THIS exactly", "preserve the pod in the reference") more restrictively than generation-style prompting ("in the style of..."). Combine cropped refs with edit-style language when you need exact matching.

### L8 — Palette consistency within same world/time must be explicit; ref images lock composition, not palette
**Tier:** Meso (cross-shot discipline with narrative consequence)
**Status:** `pending (1/3)` — validated once on DHYANA #08 v2; needs 2 more
**Context:** DHYANA flashback scenes — #04 (mother walking into upload center) and #08 (upload exterior) both supposed to be the same location at the same pre-dawn moment. User caught that #04 had warm pink-amber memory palette while #08 had cool clinical blue palette — two very different moods for what should be the same scene.
**Mistake:** When regenerating #04 with #08 as architecture ref, assumed palette would inherit from the ref image. It didn't — model used ref for composition/geometry only, re-decided palette from prompt. Prompt said "pre-dawn" but gave Nano too much latitude.
**Why it happened:** Confused "reference locks visual identity" with "reference locks EVERY visual attribute". Palette is a separate axis that needs its own anchor or explicit instruction. Vague terms like "pre-dawn" or "dusk" interpret wildly across generations.
**Result:** Two flashback shots read as different times/moods — audience would be confused about whether they're even the same location.
**Fix:** Explicit palette statement in prompt: name the exact color gradient ("warm pink fading to pale amber, warm ground fog, NO cold blue") + state what palette should be matched from ref image + negative-state the wrong palette. When using multiple refs, tell the model which ref dictates palette vs. which dictates architecture vs. which dictates character.
**Broader rule:** A single world-time has a palette. All shots in that world-time must share it. Cross-world-time deliberately differs (e.g., present cyan vs memory amber) — this is cinematography, not drift. When reviewing a set, group shots by world-time first, then check each group internally for palette consistency separately.
**Applied:** #08 v2 (regenerated warm memory palette matching #04).

### L7 — Deliverables must be packaged as reviewable artifacts, not raw file dumps
**Tier:** Macro (changes delivery workflow)
**Status:** `pending (0/3)` — just codified from DHYANA Tier 2 review friction
**Context:** DHYANA Tier 2 — 22 images generated with file names like `g15b.jpeg`, `g19a.jpeg`. User was expected to open each file individually in a folder, match it mentally to which shot it represents in the story, and decide if it was correct.
**Mistake:** Delivered the batch as "22 files in a folder, here are the paths". No visual summary. No Thai labels. No shot→story mapping. Placed 100% of the review-assembly cost on the user.
**Why it happened:** Treated "generated and organized" as "delivered". Assumed filenames were self-explanatory. Did not consider the user's actual workflow for reviewing a batch.
**Result:** User couldn't efficiently review because they had to: (a) open folder, (b) open each file, (c) remember which shot is which, (d) decide if correct. Review became tedious and error-prone.
**Fix:** For any batch of >3 images/artifacts, package deliverables as a *reviewable artifact* — an HTML storyboard, PDF, Markdown with embedded images, or similar — that presents each image INLINE with: (a) clear label (Act/Scene/Shot), (b) short Thai/user-language description of what it shows, (c) narrative context (where in the story this shot falls), (d) pair grouping for related shots. User opens ONE file, sees everything in order, can review efficiently.
**Broader rule:** "Delivered" means "user can review without extra assembly work on their part". Raw file dumps are not deliverables. If you generate N images, produce the reviewable artifact that shows all N at once, labeled and contextualized.
**Applied:** DHYANA Tier 1+2 HTML storyboard (base64-embedded thumbnails, opened via `open` command in browser) — validated once (1/3). Confirmed: browser `open` is the correct delivery; Claude Code preview panel doesn't render base64 the same way.
**Additional rule:** When producing HTML for user review, default to `open <path>` after write — don't rely on Claude Code preview panel.

### L6 — Different characters in similar contexts must be made visibly distinct in the prompt
**Tier:** Meso (per-shot discipline with narrative consequence)
**Status:** `pending (1/3)` — validated once on DHYANA g10a v2; needs 2 more
**Context:** DHYANA g10a (generic pod sleeper in Act 3) and g15b (specifically the mother's pod in Act 4). Both rendered as "neutral adult face sleeping in pod" — model gave both roughly-similar-looking adult women. User could not distinguish them, which would destroy the Act 4 reveal ("he finds his mother among thousands") because viewers would think he already saw her in Act 3.
**Mistake:** Assumed "generic neutral adult" description was sufficient for the background character (g10a). Did not specify immutable features to distinguish from the specific character (g15b mother).
**Why it happened:** When one character is "generic" and another is "specific", prompting only the specific one forces the model to invent features for the generic one — often landing on a similar default, especially when both share context (same pod, same pose, same lighting).
**Result:** Two characters that should read as clearly different people look like they might be the same person. Plot-critical reveal is at risk.
**Fix:** Even for "generic" background characters, specify immutable distinguishing features (gender, ethnicity, hair color/length, facial structure) that guarantee a viewer can't confuse them with the specific/important character in the same set. Phrase in negative as well: "this is NOT the [other character] — specifically a man with grey hair, not a woman with dark hair".
**Broader rule:** The self-review checklist must cross-check pairs of shots featuring different-but-similar-context characters. Not just "does character A stay consistent across A's shots" but "does character A look different from character B".
**Applied:** g10a v2 — regenerated as adult male with grey hair, clearly different from g15b mother.

### L5 — Back-view character refs cannot lock face identity; create front-view/face anchors separately
**Tier:** Meso (per-shot discipline with cross-shot consequence)
**Status:** `pending (0/3)` — just codified from DHYANA Tier 2 g20b failure
**Context:** DHYANA Tier 2 five shots (g15b, g19a, g19b, g20a, g20b) show the mother's face sleeping inside a pod. All five used `04_mother_back.jpeg` as character reference — but #04 is a BACK-view with hood up, face invisible. Model had no face to lock identity against.
**Mistake:** Assumed a character ref image is universally usable for identity locking. Didn't check whether the ref actually shows what the new shot needs to match.
**Why it happened:** Reference-chain thinking at the level of "which character" rather than "which feature of the character". Mother back-view refs wardrobe (indigo wool) but not face. When a future shot needs FACE consistency, a back-view ref is useless for that dimension.
**Result:** g20a and g20b render two different adult faces in the same pod (different people) — breaks first/last-frame interpolation. Five Tier 2 shots need regeneration.
**Fix:** For any character who will appear in multiple views (back, profile, front, in container), generate dedicated anchor images per view needed: one front/face anchor, one profile anchor, one back anchor. Ref the RIGHT anchor for each shot based on what feature must be locked. If only back-view ref exists and a future shot needs face, generate the face anchor BEFORE generating that shot.
**Broader rule:** When planning ref chain, ask "what does this shot need to match — face? wardrobe? pose? location? light?" Then pick refs that actually contain that feature. Back-view refs cannot teach face; macro-light refs cannot teach composition.
**Applied:** (pending) Creating `13_mother_face_in_pod.jpeg` as Tier 1 face anchor, then regenerating 5 Tier 2 shots with it.

### L4 — Self-review before showing output prevents obvious failures from reaching the user
**Tier:** Macro (workflow-level — changes delivery cadence)
**Status:** `pending (0/5)` — just codified, needs validation across 5 batches
**Context:** DHYANA Tier 1 delivery.
**Mistake:** Rendered 12 images, renamed, and showed them to user without scanning for issues myself. User caught the face-orientation problem on #7 that I should have caught first.
**Why it happened:** Treated "generate succeeds, file downloads" as completion. Skipped the step of actually LOOKING at each image with a critical eye.
**Result:** User did my QA for me. Waste of their attention.
**Fix:** After every batch, view each image, scan against the Post-generate Self-review checklist. Flag issues, regen, THEN show user.
**Applied:** This skill itself. Will run self-review on every batch going forward.

---

## CORE PRINCIPLES

These don't change between LVs. They're the spine.

1. **Mismatch between shots beats beauty per shot.** A perfect #1 and a perfect #2 that don't match is worse than two adequate shots that match.
2. **Ambiguity = model's choice, not yours.** Every unstated detail is a coin-flip. State everything that matters; accept the rest as generative surprise.
3. **Reference images are not optional polish — they're foundational.** For any multi-shot project, ref chains should be designed BEFORE the first generation.
4. **Numbers > adjectives.** "2.1 meter" not "long". "85mm" not "telephoto". "40 rack columns" not "many racks".
5. **Negative-state the common failures.** "No age markers, no text, no watermark, no [specific model failure mode you've seen before]".
6. **Self-review is not optional.** It is the last step of generation, not a nice-to-have.

---

## LEVELING PROTOCOL

### Validation Gate (mandatory before LV up)

Before a lesson can be promoted from `pending` to `validated`, and before the level bumps, it must pass tiered validation:

| Tier | Definition | Required tests | Pass threshold |
|------|-----------|---------------|----------------|
| **Micro** | Small phrasing/naming/convention change, low blast radius | 1 | 1 of 1 |
| **Meso** | Technique affecting a single shot/image (e.g., face orientation, opacity spec) | 3 | 2 of 3 |
| **Macro** | Workflow-level change affecting whole projects (e.g., ref chain dependency graph) | 5 | 3 of 5 |

**Status field on every lesson:**
- `pending (X/Y)` — still being validated, X tests logged out of Y required
- `validated` — passed threshold, now safe to rely on
- `retired` — superseded by newer lesson or proven wrong (keep for history, mark the reason)

**Process:**
1. New mistake observed → log lesson immediately as `pending (0/Y)` — don't wait.
2. Each subsequent time the lesson is applicable: apply the fix, record pass/fail in a validation log on the lesson itself.
3. When X reaches Y: if pass threshold met → promote to `validated` AND bump LV. If not met → rewrite the lesson (what actually works differs from first guess), reset validation counter.
4. Never bump LV without at least one `pending → validated` promotion in the changelog.

**How to classify a new lesson:**
- Blast radius = "if this fix is wrong, how many future generations break?"
- Small single-prompt tweak = Micro. Per-shot discipline = Meso. Changes workflow = Macro.
- When unsure, pick the higher tier.

### When to level up

You level up when ≥1 `pending` lesson promotes to `validated` AND it's substantial enough to meaningfully change future work. Trivial wins stay as micro-lessons without a level bump.

**On level up:**
- Bump `level:` in frontmatter
- Add changelog entry with date, validated lesson(s), and 1-line "what this unlocks"
- git commit the SKILL.md with message `LVN: <validated lesson summary>`

### Rollback

Skill is under git at `~/.claude/skills/prompt-craft-lv/`. If a lesson promotion turns out wrong:
- `git log SKILL.md` to see history
- `git revert <sha>` to undo a bad promotion cleanly (keeps history)
- Document the rollback reason in a new changelog entry — don't hide it

**Never silently edit old lessons or changelog entries — they're history. Use retired status or git-revert.**
