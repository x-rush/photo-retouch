# photo-retouch

Professional portrait-retouching methodology pack for AI coding agents (SKILL.md-compatible: Claude Code, ZCode, …), distilled from real client-photo retouching sessions with generative editing models.

**The contract**: correction work = one generation per photo. Read everything up front (bystanders counted, clutter itemized, color direction designed, facial flaws enumerated), compose one final prompt, generate once, then return the image with an 8-point identity-anchor verification and honest suggestions. Never auto-regenerate; never invent suggestions when the result is clean.

## Three edit classes

| Class | Covers | Discipline |
| --- | --- | --- |
| **A · Correction** (default) | retouch, de-clutter, de-person, color, skin | Full identity lock; single-shot; 8-point anchor checklist |
| **B · Re-imagination** | 换动作 / 换视角 / 换表情 / pose & camera-angle change | Face locked, pose free; one transformation per turn; multi-turn; judged by anchors (SSIM expected low) |
| **C · Expansion** | 扩图 / uncrop / extend background / aspect change | Original pixels invariant; new canvas continues era, light, perspective |

Class B is backed by modern instruction models (Nano Banana 2.1 officially supports identity-preserving pose & camera-angle edits, improved multi-turn stability in 2.1).

## Inside

- **Six iron rules** — read-before-acting (native vision required), class-based pacing, one final prompt for correction, identity lock (appearance descriptions, never ethnicity names), the reshaping red line scoped to Class A, honest acceptance ("good as is" when clean — never invent suggestions)
- **Exhaustive analysis worksheet** — region-by-region scan: bystanders counted (reflections & distant figures), clutter itemized, element keep/remove via **four professional tests** (gaze / era-narrative / information / space), facial flaws **enumerated region-level** (nasolabial folds, acne, dark circles, redness, stray hairs, oil shine), skin-tone continuity (face = neck = hands), EXIF-true aspect ratio
- **Color grading playbook** (`reference/color-grading.md`) — HSL skin science (orange/yellow desaturate + brighten), six style recipes (Japanese fresh / Korean clean / film / premium teal-orange / HK retro / airy Chinese style), warm-cool separation formula, generative phrasing discipline
- **Capability boundary disclosure** — frequency-separation skin work, dodge & burn, per-eye retouching are professional-manual territory; the skill tells users what's out of scope upfront
- **Pitfall archive** — five paid-for failures and the rules they produced

## Requirements

- Session model with **native vision** (the analysis step is invalid via relay description tools)
- An image-editing backend — pairs with **[image-forge](https://github.com/x-rush/image-forge)** (multi-provider generation CLI, fal.ai + Replicate); any instruction-editing capability works

## Cost profile

Correction work ≈1 generation per photo (user-approved rework rounds extra). See the companion engine for per-model pricing (retouch tier ≈$0.08/img).

## License

MIT
