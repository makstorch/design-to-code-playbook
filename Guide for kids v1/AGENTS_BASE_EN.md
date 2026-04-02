# AGENTS_BASE.md
Version: v1.1
Purpose: reusable working rules for transferring designs from Figma to production-ready code.

---

## 1) Mission
Build UI from Figma so that the result is:
- visually accurate;
- stable across breakpoints;
- safe for existing project logic;
- easy to maintain after handoff.

Primary quality threshold:
- matches the structure and behavior from Figma;
- no regressions in untouched blocks;
- changes are easy to verify and roll back.

---

## 2) Priorities (if rules conflict)
1. Do not break working behavior.
2. Stay within the agreed scope.
3. Preserve visual parity with Figma.
4. Reuse the current architecture before adding new patterns.
5. Keep implementation simple and maintainable.

---

## 3) Scope and change discipline
### 3.1 Scope first
- If the task is local (for example, only `Menu`), do not change unrelated blocks.
- Small adjacent fixes are allowed only as a direct consequence of the task.
- Any extended refactor requires explicit agreement with the user.

### 3.2 Reuse first
Before writing new code, check whether existing pieces can be extended:
- components/blocks;
- CSS tokens and utilities;
- current media query strategy;
- existing JS logic (dropdown, modal, i18n helpers).

Do not rewrite a working block just for cosmetic unification.

### 3.3 Incremental delivery
Work in small change sets:
1. Analyze the current implementation.
2. Define a short plan.
3. Implement one logical change set.
4. Validate behavior.
5. Move to the next change set.

---

## 4) Figma as the source of truth
Use Figma as the canonical visual source:
- Dev Mode;
- structure and values via MCP;
- named frames/states;
- exported assets.

Do not use screenshots as the primary source if layer structure is available.

### 4.1 Frame naming convention
Expected format:
`<Block> <State> [<Breakpoint> · <Theme>]`

Example:
`Menu Default [1920 · Light]`

### 4.2 States to verify (if present in design)
- Default
- Hover
- Active
- Disabled
- Layout/resizing behavior

`Layout` frames are a behavioral specification, not optional reference material.

---

## 5) Responsive requirements
Minimum checkpoints:
- 1920
- 1280
- 768
- 375

Rules:
- do not make a desktop-only implementation;
- avoid horizontal overflow unless it is intentional;
- preserve spacing rhythm and section geometry at every breakpoint.

---

## 6) Asset rules
Preferred formats:
- icons: SVG;
- raster: PNG/WebP;
- high-density support: @2x/@3x when needed.

When replacing assets:
1. Connect the new file in markup/styles.
2. Verify displayed size and Retina quality.
3. Make sure the old asset is not used anywhere else.
4. Remove the old asset only after usage verification.

---

## 7) Interactions and accessibility
For interactive UI, at minimum verify:
- behavior with keyboard and mouse/trackpad;
- visible focus states;
- correct state transitions (default/hover/active/disabled);
- no broken ARIA label/role behavior after changes.

For modals:
- close on overlay click;
- close on `Esc`;
- close via close button;
- correct focus behavior.

---

## 8) Localization rules
- Any new user-facing text must go through i18n.
- Do not leave permanent hardcoded strings in feature code.
- Keep a consistent translation key style.
- Fallback language is a safety net, not a replacement for full translations.

---

## 9) Browser validation strategy
### 9.1 Mandatory
- Chromium-based browser (latest stable)
- Safari (latest stable desktop)

### 9.2 Conditionally mandatory
- Safari iOS for release-critical or layout-sensitive changes.

High-risk areas in Safari:
- fixed/sticky positioning;
- scroll containers and clipping overflow;
- modal overlay;
- viewport units (`vh`/`dvh`);
- SVG and Retina rendering;
- flex min-size behavior.

---

## 10) Definition of Done
Before completing the task, verify:
- visual result matches Figma within the request scope;
- behavior is correct at mandatory breakpoints;
- no regressions in adjacent blocks;
- i18n and accessibility are not broken;
- modified files pass lint/checks;
- assets and links are valid.

---

## 11) Response format before implementation
Before making changes, show:
1. Plan (short, step by step)
2. Which files will be changed
3. Risks
4. Verification checklist

Keep wording concise and practical.
