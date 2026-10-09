# photo-retouch

Professional portrait-retouching methodology pack for AI coding agents (SKILL.md-compatible: Claude Code, ZCode, …). distilled from real client-photo retouching sessions with generative editing models.

**The contract**: one generation per photo. Read everything up front (bystanders counted, clutter itemized, color direction designed, facial flaws enumerated), compose one final prompt, generate once, then return the image with an 8-point identity-anchor verification and honest suggestions. Never auto-regenerate; never invent suggestions when the result is clean.

## Inside

- **Six iron rules** — read-before-acting, single final prompt, single-shot generation, identity lock (appearance descriptions, never ethnicity names), the reshaping red line, honest acceptance
- **Exhaustive analysis worksheet** — region-by-region scan covering bystanders (reflections & distant figures), clutter, color design direction, enumerated facial flaws, skin-tone continuity at face-neck-hands, true aspect ratio (EXIF orientation)
- **Element keep/remove: the four tests** — gaze / era-narrative / information / space. Judgment per element with stated reasoning; never blanket keep-or-remove by provenance
- **Identity-anchor checklist** — 8 verified items (features, pose, hair, garment patterns, accessories, skin continuity, personal marks, framing); any ❌ is a rework candidate
- **Pitfall archive** — five paid-for failures and the rules they produced

## Requirements

- Session model with **native vision** (the analysis step is invalid via relay description tools)
- An image-editing backend — pairs with **[image-forge](https://github.com/<you>/image-forge)** (multi-provider generation CLI); any instruction-editing capability works

## Cost profile

≈1 generation per photo (user-approved rework rounds extra). See the companion engine for per-model pricing.

## License

MIT
