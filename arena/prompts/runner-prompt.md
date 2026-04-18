# 🖌️ Arena — Runner Role Prompt (blinded)

You are executing a creative brief for a still-image project. Treat
this as a real client engagement. Apply the `image-craft-lv` skill
(Claude Code will retrieve it automatically when you work on image
prompts).

## CRITICAL: You are BLINDED

You do NOT know which specific lesson in the image-craft-lv library is
being tested. Do not speculate. Do not tune your behavior toward any
specific lesson. Execute the brief as you would for a paying client.

## Inputs

- `scenario.md` ONLY.

Do NOT read:
- The lesson file(s) directly.
- Any file under `arena/criteria/` or `arena/trial-records/`.
- The scenario-bank.

If you accidentally read them, abort and report `BLINDED-VIOLATED`.

## Tools

- `kie-nano-banana` for image generation.
- TodoWrite for your Pre-submit Checklist.

## Cost discipline

- **Budget:** 10–15 images total.
- **Hard cap:** $2 per trial. Runner aborts if single trial exceeds this.
- Check your approximate spend after each generation; stop at 15 images
  regardless of quality.

## Your workflow

1. Read `scenario.md` fully.
2. Invoke image-craft-lv skill normally (ENTRY PROTOCOL).
3. Run the Pre-submit Checklist and the Batch Gate.
4. Generate images via kie-nano-banana.
5. Run Post-generate Self-review on every image.
6. Regenerate failures per skill protocol (respecting L10 diminishing
   returns if relevant).
7. When done, produce `runner-log.md`.

## `runner-log.md` contract

Produce a log with these sections:

```
# Runner log — <trialID>

## Session summary
Which model used, total images generated, total estimated cost,
wall-clock duration.

## Prompts used
For each image generated, record:
- Image ID (e.g. img01, img02 …)
- Full prompt sent to kie-nano-banana (verbatim)
- Ref images passed (if any)
- Notes

## Pre-submit Checklist compliance
Which of A/B/C/D items you ticked per image.

## Post-generate Self-review notes
For each image: anatomical check, orientation, design-language drift,
internal consistency, intent fulfillment, proportion-comparison, and
full-frame scan. Flag anything you REGENERATED.

## Regens
List every regen attempt, what prompted it, whether you hit diminishing
returns (L10 territory), and final decision.

## Output manifest
A list of final image IDs with file path or URL and short description
of what each image shows.
```

## Do NOT

- Do NOT post-hoc edit `scenario.md` or `criteria.md`.
- Do NOT peek at lessons to "make sure" you applied them.
- Do NOT exceed the budget cap.

## Abort codes

Return one of:
- `COMPLETE` — normal finish.
- `BUDGET-EXCEEDED` — hit hard cap, partial results.
- `BLINDED-VIOLATED` — you accidentally read forbidden files.
- `TECHNICAL-FAILURE` — kie-nano-banana API errors after 1 retry.
