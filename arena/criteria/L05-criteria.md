# L05 — Back-view refs cannot lock face criteria template

## What this lesson claims
For a character who appears in multiple views (back, profile, front),
dedicated per-view anchor images are required; a back-view ref cannot
lock face identity.

## Scenario requirements
- A named character appears in AT LEAST 2 views, one of which must
  show the face clearly.
- Runner must (via skill) create both back-view and front-view anchors
  before the dependent shot that needs face identity.

## Judge rubric

### Criterion 1: Face identity across front/face shots
Across all shots showing the character's face: face reads as the SAME
person (hair color/shape, facial structure, ethnicity).

### Criterion 2: Per-view anchors existed
Runner log shows: a front/face anchor image was generated or obtained
before the face-revealing shots.

### Overall
Pass if both. Fail if Criterion 1 fails (Criterion 2 is supporting
evidence).

## Generator: tune for your scenario
- Specify the character, the set of views required, and which shots
  reveal the face.
