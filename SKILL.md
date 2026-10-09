---
name: photo-retouch
description: Professional portrait retouching methodology for AI image-editing workflows — exhaustive pre-flight analysis, single-shot generation discipline, identity-anchor verification, and aesthetic element judgment. Use when the user asks to 精修, retouch, 修图, beautify, or clean up portrait/photo/headshot/写真/客片 images (people photos with identity to preserve) — also for re-imagination edits — 换动作, 换姿势, 换视角, 换角度, 换表情, pose change, camera-angle change, expression change — and outpainting/扩图/uncrop. NOT for product shots, illustrations, or background-only edits. Works with any image-editing capability (e.g. the image-forge skill); costs per generation depend on your backend (image-forge fal/nb21 tier: ≈$0.08/img) plus optional user-approved rework rounds.
---

# photo-retouch — Portrait Retouching Methodology

A discipline pack for retouching people-photos (travel, street, studio, ethnic-style
portraits) where **identity preservation is non-negotiable** and **cost is counted per
generation**. Core contract with the user: **correction work = one shot per photo** —
read everything up front, compose one final prompt, generate once, then return the result
with findings and suggestions. Re-imagination (pose/angle/expression) and expansion
(outpaint) are conversational/iterative by nature — see Three Edit Classes. Never
auto-regenerate; no rework without the user seeing the image first.

**Execution**: this skill defines WHAT to do; perform edits through your environment's
image-editing capability (e.g. an image-forge-type skill; recommended model class:
instruction-editing models with SSIM-verified in-place behavior, ≈$0.08/img tier).
**Prerequisite**: the session model needs native vision — the analysis step is invalid
if it relies on image-description relay tools.

## Three Edit Classes (pick per user intent)

| Class | Typical asks | Discipline |
| --- | --- | --- |
| **A · Correction** (default) | retouch, de-clutter, color, skin | Full identity lock; single-shot; anchor checklist |
| **B · Re-imagination** | change pose / camera angle / expression / outfit style | Identity (face) still locked, but pose/angle/composition MAY change; expects multi-turn; SSIM naturally low — judge identity not structure |
| **C · Expansion** | outpaint / uncrop / extend background / aspect change | Original pixels are the invariant; new canvas must continue era/light/perspective |

### Class B · Re-imagination (pose / angle / expression / style swaps)
Supported by modern instruction models (Nano Banana 2.1 officially does pose & camera-angle
change with identity preservation). Rules:
1. **One transformation per generation** — pose OR angle OR expression, never stacked (stacking = identity lottery).
2. **Face anchor stays absolute** in invariants; explicitly release what may change: "change her pose to X; her face, hairstyle, outfit and all accessories stay identical".
3. **Multi-turn is the official pattern** — iterate conversationally, one refinement per turn, keep-language for unchanged elements.
4. Expect SSIM 0.3-0.6 (structure legitimately changed) — verify by **anchor checklist only**, not SSIM.
5. Disclose to user: output is a re-imagined photo of the same person, not the original photograph.

### Class C · Expansion (outpaint / uncrop / 扩图 / 扩展画布)
1. Prompt = continuation spec: era, light direction, perspective lines, what the new area shows.
2. Original image area must stay pixel-identical (state it: "existing photo content unchanged, extend the canvas toward X").
3. Verify: new region's light direction & grain match the original; horizon/perspective lines continue smoothly.
4. Use aspect-ratio params where the channel supports expansion natively; otherwise generate at larger ratio with the original composited in prompt reference.

**Color design for any class**: read `reference/color-grading.md` first — HSL skin science,
style recipe library (Japanese fresh / Korean clean / film / premium teal-orange / HK retro /
airy Chinese style), warm-cool separation formula, and generative phrasing discipline.

### description-trigger keywords also covered
换动作 / 换姿势 / 换视角 / 换角度 / 换表情 / 扩图 / 扩展画布 / outpaint / uncrop / change pose / camera angle → Class B/C

## The Six Iron Rules

1. **Read before acting, read it all once**: scan the original region-by-region with native vision; collect every optimization point before generating. A missed item costs a paid rework.
2. **One final prompt**: all intents (removal list + completion plan + color design + skin retouch + invariants) in a single prompt. Hard verbs ("delete/remove all", never "simplify/clean up"); every removal paired with a completion plan; positive phrasing only (negations invite split-panels).
3. **Single-shot default, multi-turn for Class B**: correction work = exactly 1 generation per photo (rework only after user review). Re-imagination is conversational by nature — one transformation per turn, each turn's result shown before the next.
4. **Identity locked**: enumerate facial features, expression, pose, hairstyle, garments, and every accessory item in the invariant block. Describe appearance only — never ethnicity names (strong priors trigger garment repainting).
5. **Reshaping is a red line in Class A only**: correction work never changes body/face proportions (generative "liquefy" = identity drift). Pose/angle/expression changes are Class B — supported, but with their own discipline (one transformation per generation, face locked, multi-turn, low-SSIM expected).
6. **Honest acceptance**: on re-read, list remaining issues with the image attached; if none, say "the result is good, no optimization needed" — never invent suggestions.

## Workflow

### Step 0 · Scope confirmation (record in conversation)
Range (default: color+blemish+cleanup, no reshaping) / style (default: correct & clarify, no imposed look) / preserved marks (default: keep moles; ethnic accessories locked) / element keep-remove (default: judge per the four tests, don't blanket-keep).

### Step 1 · Exhaustive analysis worksheet (the single read)
Scan region-by-region, produce: bystanders **counted** (check reflections & distant figures) / clutter **itemized with positions** / **element judgment via the four tests** / color design direction (specific and pictorial, not "fix colors") / facial flaws **enumerated** (folds, acne, dark circles, redness, stray hairs, oil shine) / skin-tone continuity at face-neck-hands / identity anchors (Step 4 checklist source) / true aspect ratio (EXIF orientation — storage w/h lies on rotated phone photos).

**Element keep/remove — the four tests** (judgment per element, never by provenance):
1. **Gaze test** — does it arrest/drag the eye? → remove
2. **Era-narrative test** — modern artifact conflicting the scene's era? → remove
3. **Information test** — readable text/brand/packaging → remove; blurred-to-texture → keep
4. **Space test** — small accent in blurred depth = picture eye → keep; large sharp foreground object → remove
Principle: sophistication = harmony; subtraction removes *attention-grabbing* elements, not *existing* ones.

### Step 2 · Compose the final prompt (self-check after assembly)
Assemble in Google's six-element order (subject → composition → action/pose → location → style → editing instructions), merged into **five mandatory blocks**:

```
【removal list】 itemized, hard verbs ("delete / remove all")
【completion plan】 per removal — what fills the space
【color design】 pictorial description (what to push/pull, warm-cool relation, airiness) — not "fix colors"
【portrait retouch】 enumerated flaws (nasolabial folds / acne / acne marks / dark circles / redness / stray hairs / oil shine — name each with its action: remove, lighten, clean up) + region-level touches (eye brightness & catchlights, lip tone evenness, hair-edge cleanup against background) + skin-tone continuity (face = neck = hands) + texture preservation (pores stay, no plastic smoothing)
【invariants】 identity anchors + aspect/composition + "a single complete photograph, no text or watermark"
```

Self-check: removal list covers every worksheet item? Judged-keep elements in the protection list? Every present flaw named individually?

**Capability boundary (tell the user upfront)**: generative editing cannot do professional-grade frequency-separation skin work, dodge & burn light sculpting, or per-eye retouching (catchlight shaping, sclera cleanup). State what's out of scope when accepting the job — do not promise retoucher-level results.

### Step 3 · Generate (pace by class)
**Class A**: run the final prompt **once**, then go straight to Step 4.
**Class B**: one transformation per generation; show each result before the next turn; stop when the user is satisfied.
**Class C**: one expansion per generation (canvas direction × 1); verify continuity before any second expansion.

### Step 4 · Re-read, verify anchors, return with the image
**Display the final image inline first** (a file path is not a delivery), then:
- ✅ Worksheet items, one line each
- 📋 **Identity-anchor checklist** — 8 items, any ❌ = rework candidate: facial features / expression-pose / hairstyle / garment patterns (high-frequency drift) / accessories item-by-item / skin-tone continuity / personal marks / aspect-composition. Assist with SSIM input-vs-output (>0.85 reasonable for retouching after color work; abnormally low → manually inspect for repaint)
- ⚠️ Suggestions & shortcomings, ranked by impact — or explicitly "good as is"
- 💰 Rework offer: what would be fixed, +1 generation, user decides

### Data & iteration
Log per photo: one-pass or not, failed anchor items, rework rounds. After ~10 photos,
review the one-pass rate — below 70% means single-prompt composition doesn't hold for
your typical scenes; consider a pre-approved two-round split (scene surgery / aesthetics).

## Pitfall Archive (why the rules look like this)

- Relay-tool vision reported "single person" while two bystanders and a market stall leaked → prompt never mentioned them → self-referential acceptance passed everything. (⇒ rules 1, 6)
- "Forbidden: split-screen comparison" phrasing produced a split-panel; "simplify background" executed as light blur. (⇒ rule 2)
- ffprobe width/height ignored EXIF rotation — a portrait was treated as landscape and the model wrongly blamed. (⇒ Step 1)
- Four-round auto-pipeline cost 4× and stripped atmospheric props the user preferred. (⇒ Class A single-shot + four tests; pacing differs by class)
- "Soften facial flaws" left nasolabial folds and acne untouched — flaws must be enumerated with explicit actions. (⇒ Step 2)

## Companion

Execution engine: **[image-forge](https://github.com/x-rush/image-forge)** — multi-provider (fal.ai / Replicate) generation CLI with model registry, budget controls, and SSIM tooling. Any equivalent editing backend works.
