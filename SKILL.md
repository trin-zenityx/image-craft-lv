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

1. **Anatomical plausibility** — pod proportions, body in pose, scale of figure vs environment. If a 2m pod looks like a 60cm capsule, flag it.
2. **Orientation** — does the face point where you intended? Hand pose match ref?
3. **Design-language drift** — does the opaque-body pod in shot A still look opaque in shot B of the same set? Did the character's robe change color?
4. **Within-image internal consistency** — is the light direction consistent with the shadows? If a window is to the left, is the rim light coming from the left?
5. **Intent fulfillment** — reread your own prompt's key phrases. Does the image show "weathered hands with cyan rim"? Or just generic hands?

**If anything fails: regenerate with a fix, don't ship the broken version hoping user won't notice.**

---

## LESSONS LIBRARY

Concrete mistakes + fixes. Grows over time. Always include: **Context, Mistake, Why it happened, Fix, Applied evidence.**

### L1 — Reference chains beat text-only for multi-shot sets
**Context:** DHYANA project Tier 1 round 1 — 12 anchor images for a 25-shot short film.
**Mistake:** Generated all 12 with text-only prompts. Relied on verbal repetition ("saffron robe, shaved scalp, weathered olive-tan skin") to keep Tenzin's face consistent across #1 frontal and #2 profile.
**Why it happened:** Assumed prose repetition was sufficient. Didn't think about model's stochastic interpretation per call.
**Result:** Face drifted — #1 Tenzin and #2 Tenzin were clearly different people. Cathedral in #5 and pod corridor in #6 had different architectural language.
**Fix:** Build dependency graph. Generate master anchors first (no refs). Generate secondary with master refs. Generate tertiary with master + secondary refs. Per the Nano Banana skill, pass `--reference path/to/anchor.png` as many times as needed.
**Applied:** Tier 1 v2 (all 12 regenerated). Face locked. Architecture locked. Pod design locked.

### L2 — Face orientation inside containers must be explicit
**Context:** DHYANA #7 pod detail — full-body pod, sleeping face visible through face-window.
**Mistake:** Wrote "the calm sleeping face of an adult human, visible through the frosted face-window". Did not specify which way the face was oriented.
**Why it happened:** Human logic says "if face is visible through window, face is probably turned to window" — but that's the model's assumption, not your intent. Your intent was "supine body, face up to ceiling, visible through top-mounted porthole".
**Result:** Multiple versions of #7 came back with face turned sideways toward the glass, looking awkward and inconsistent with #6 where other pod faces were oriented up.
**Fix:** Always state face direction explicitly: "face turned UPWARD to the ceiling, body supine, face visible through the window from above" or "face turned forward to camera at three-quarters" — never leave it unstated.
**Broader rule:** Any time a face/body is seen through a window/mirror/transparent surface, specify (a) subject orientation, (b) camera position relative to subject, (c) what viewer sees through the glass.
**Applied:** #7 v5 (pending at time of logging).

### L3 — Opaque vs transparent container surfaces must match across the set
**Context:** DHYANA pods — #6 corridor and #7 detail.
**Mistake:** Said "transparent/frosted panels" in the detail prompt, same subject but different word choice than corridor prompt. Model rendered #6 with entirely opaque bodies (only face-window) and #7 with transparent-torso panels.
**Why it happened:** Vague wording + no cross-shot design-language statement. Each prompt re-decides the design.
**Fix:** In any multi-shot prompt set, pick one unambiguous phrase for each surface treatment and use it identically: "completely OPAQUE white ceramic shell along entire body, with face-window as the only transparent surface". Then mirror it exactly in every prompt that features that object.
**Applied:** #7 v4 (opaque body, face-window only) — matched #6.

### L4 — Self-review before showing output prevents obvious failures from reaching the user
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

You level up when:
- You make a new mistake, diagnose it honestly, and add a Lesson here.
- You apply an existing lesson successfully across 3+ uses without drift.
- You discover a new capability of a model (new refs, new modes) that changes the playbook.

When leveling: bump `level:` in frontmatter, add a changelog entry, and write the new Lesson with all five fields (Context, Mistake, Why, Fix, Applied).

Never silently edit old lessons — they're history.
