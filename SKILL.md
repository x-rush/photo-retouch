---
name: photo-retouch
description: Professional portrait retouching methodology for AI image-editing workflows — exhaustive pre-flight analysis, single-shot generation discipline, identity-anchor verification, and aesthetic element judgment. Use when the user asks to 精修, retouch, 修图, beautify, or clean up portrait/photo/headshot/写真/客片 images (people photos with identity to preserve) — NOT for product shots, illustrations, or background-only edits. Works with any image-editing capability (e.g. the image-forge skill); costs ≈$0.08 per image plus optional user-approved rework rounds.
---

# photo-retouch — Portrait Retouching Methodology

A discipline pack for retouching people-photos (travel, street, studio, ethnic-style
portraits) where **identity preservation is non-negotiable** and **cost is counted per
generation**. Core contract with the user: **one shot per photo** — read everything up
front, compose one final prompt, generate once, then return the result with findings and
suggestions. Never auto-regenerate; no rework without the user seeing the image first.

**Execution**: this skill defines WHAT to do; perform edits through your environment's
image-editing capability (e.g. an image-forge-type skill; recommended model class:
instruction-editing models with SSIM-verified in-place behavior, ≈$0.08/img tier).
**Prerequisite**: the session model needs native vision — the analysis step is invalid
if it relies on image-description relay tools.

## The Six Iron Rules

1. **Read before acting, read it all once**: scan the original region-by-region with native vision; collect every optimization point before generating. A missed item costs a paid rework.
2. **One final prompt**: all intents (removal list + completion plan + color design + skin retouch + invariants) in a single prompt. Hard verbs ("delete/remove all", never "simplify/clean up"); every removal paired with a completion plan; positive phrasing only (negations invite split-panels).
3. **Single-shot**: default exactly 1 generation per photo. Rework rounds happen only after the user reviews the output and names a suggestion (+1 generation each).
4. **Identity locked**: enumerate facial features, expression, pose, hairstyle, garments, and every accessory item in the invariant block. Describe appearance only — never ethnicity names (strong priors trigger garment repainting).
5. **Reshaping is a red line**: no body/face proportion changes by default (generative "liquefy" = identity drift). If explicitly requested: isolated round, disclosed risk.
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
Five blocks in order: 【removal list】itemized hard verbs → 【completion plan】per removal → 【color design】pictorial description → 【portrait retouch】skin (with face-neck-hand continuity) + enumerated flaws + texture preservation → 【invariants】identity anchors + aspect/composition + "a single complete photograph, no text or watermark". Self-check: does the removal list cover every worksheet item? Are judged-keep elements in the protection list?

### Step 3 · Generate once
Run your editing capability with the final prompt. **Run it once.** Then go straight to Step 4.

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
- Four-round auto-pipeline cost 4× and stripped atmospheric props the user preferred. (⇒ single-shot + four tests)
- "Soften facial flaws" left nasolabial folds and acne untouched — flaws must be enumerated with explicit actions. (⇒ Step 2)

## Companion

Execution engine: **[image-forge](https://github.com/<you>/image-forge)** — multi-provider (fal.ai / Replicate) generation CLI with model registry, budget controls, and SSIM tooling. Any equivalent editing backend works.
