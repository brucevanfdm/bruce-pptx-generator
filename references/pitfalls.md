# QA Process & Common Pitfalls

## Step 5.5 — Pre-Compile Code Review (REQUIRED)

Run this before compiling. You cannot see the rendered output, so catch layout bugs in code.

Go through every slide JS file and check each item below. Write down every issue found — do not fix silently.

### 1. Bounds Check

Slide canvas: **10" wide × 5.625" tall**. Every element must satisfy:

```
x >= 0  AND  x + w <= 10
y >= 0  AND  y + h <= 5.625
```

Common traps:
- Page number badge at `x:9.3, w:0.4` → right edge = 9.7 ✓ (if x were 9.7 it would clip)
- A shape at `x:0.5, w:9.8` → right edge = 10.3 ✗ overflows by 0.3"
- Text at `y:5.0, h:0.8` → bottom edge = 5.8 ✗ overflows by 0.175"

**Check every element. Flag any where x+w > 10 or y+h > 5.625.**

### 2. Overlap Check

For each slide, list all element bounding boxes and check for unintended overlaps.

Two elements overlap when:
```
A.x < B.x+B.w  AND  A.x+A.w > B.x
AND
A.y < B.y+B.h  AND  A.y+A.h > B.y
```

Intentional overlaps (text on top of a background shape) are fine. Flag these unintended cases:
- Two text boxes with similar x/y that would obscure each other
- A shape that covers a text element it shouldn't
- Page badge overlapping body content (body content must end before y:5.0)

### 3. Background Consistency

All slides of the same type must share exactly the same background. Check that:

| Slide type | Expected background |
|------------|---------------------|
| Cover | Defined in Step 2 (one consistent choice for the deck) |
| TOC | Consistent with Cover or a designated variant |
| Section Divider | All dividers use the **same** background color/style |
| Content pages | **All content pages must have identical backgrounds** |
| Summary | Matches Cover or a designated closing style |

Common failure: one content slide uses `theme.bg`, another uses `"FFFFFF"` — visually identical in this palette but signals inconsistency that will break if the theme changes.

**Fix**: define a `SLIDE_BACKGROUNDS` constant at the top of compile.js and pass it through, rather than hardcoding per-slide.

```javascript
// compile.js — define once, pass to every slide
const backgrounds = {
  cover:    theme.bg,
  toc:      theme.bg,
  divider:  "EEF6FF",   // or whatever was chosen
  content:  "FFFFFF",   // ALL content pages must use this
  summary:  theme.bg,
};
```

### 4. Font Consistency

Scan every `fontFace` value in each slide file. All should be one of:
- `"Microsoft YaHei"` — for Chinese or mixed content
- The chosen English font (Arial, Georgia, etc.)

Flag any slide that uses a different font accidentally.

### 5. Color Compliance

Every color value should come from `theme.*`. Flag any hardcoded hex literals that aren't `"FFFFFF"` (white) or `"000000"` (black).

Also check: no `"#"` prefix on any hex string anywhere.

### 6. Title Structure

For each content/TOC/summary slide:
- Title text box is at a consistent y position (should be the same across all content slides, e.g. `y: 0.22`)
- Title uses `bold: true` and `color: theme.primary`
- If the style requires an accent bar (e.g. 企业科技蓝), it is present directly below the title

### 7. Page Number Badge

Every slide except the Cover must have a page number badge. Check:
- Badge is present
- Badge shows correct sequential number
- Badge position: `x: 9.3, y: 5.1, w: 0.4, h: 0.4` (or equivalent pill variant)

### 8. Cross-Slide Consistency Matrix

After checking all slides individually, do one cross-slide pass. Build a quick table in your head (or write it out):

| Slide | Type | Title y | Title fontSize | Content start y | Background |
|-------|------|---------|---------------|-----------------|------------|
| 01 | cover | — | — | — | `theme.bg` |
| 02 | toc | 0.22 | 30 | 0.9 | `theme.bg` |
| 03 | divider | — | — | — | `EEF6FF` |
| 04 | content | 0.22 | 30 | 1.0 | `FFFFFF` |
| 05 | content | 0.22 | 30 | 1.0 | `FFFFFF` |
| 06 | content | **0.3** | **28** | 1.0 | `FFFFFF` ← **flag: title y and fontSize differ** |

Flag any same-type slides where these values differ. Common inconsistencies:
- Title `y` drifts by 0.1–0.2" between slides (looks misaligned when flipping)
- Title `fontSize` varies (28 vs 30 vs 32 — pick one and use it everywhere)
- Content area start `y` inconsistent (body text starts at different heights)
- One content slide has a slightly different background hex

### How to report issues

After reviewing all slides, list findings like:

```
slide-03.js: title text box y:0.22 h:0.6 → bottom = 0.82; accent bar y:0.88 → gap is fine ✓
slide-04.js: shape at x:0.5 w:9.8 → right edge 10.3 → OVERFLOW, fix w to 9.5
slide-05.js: background "FFFFFF" but other content slides use theme.bg → INCONSISTENCY
slide-06.js: page badge missing → ADD BADGE
```

Fix all flagged issues before proceeding to compile.

---

## Post-Compile QA

**Assume there are problems. Your job is to find them.**

Your first render is almost never correct. Approach QA as a bug hunt, not a confirmation step. If you found zero issues on first inspection, you weren't looking hard enough.

### Content QA

```bash
python -m markitdown output.pptx
```

Check for missing content, typos, wrong order.

**Check for leftover placeholder text:**

```bash
python -m markitdown output.pptx | grep -iE "xxxx|lorem|ipsum|placeholder|this.*(page|slide).*layout"
```

If grep returns results, fix them before declaring success.

### Verification Loop

1. Generate slides → Extract text with `python -m markitdown output.pptx` → Review content
2. **List issues found** (if none found, look again more critically)
3. Fix issues in the source JS files, then recompile
4. **Re-verify affected slides** — one fix often creates another problem
5. Repeat until a full pass reveals no new issues

**Do not declare success until you've completed at least one fix-and-verify cycle.**

### Per-Slide QA (for from-scratch creation)

```bash
python -m markitdown slide-XX-preview.pptx
```

Check for missing content, placeholder text, missing page number badge.

---

## Common Mistakes to Avoid

### Layout & Positioning
- **Don't let elements overflow the slide** — always verify `x+w ≤ 10` and `y+h ≤ 5.625`; a shape at x:0.5 w:9.8 overflows by 0.3"
- **Don't let body content reach y:5.0+** — the page badge lives at y:5.1; body content should end by y:4.9 at the latest
- **Don't hardcode per-slide backgrounds** — inconsistent backgrounds across same-type slides are a top visual defect; define backgrounds once in compile.js and pass them through
- **Don't forget text box default margin** — PptxGenJS adds internal padding to text boxes; set `margin: 0` when aligning text precisely with shapes or icons at the same position
- **Don't use low-contrast elements** — icons AND text need strong contrast against the background

### Content & Style
- **Don't repeat the same layout** — vary columns, cards, and callouts across slides
- **Don't center body text** — left-align paragraphs and lists; center only titles
- **Don't skimp on size contrast** — titles need 36pt+ to stand out from 14-16pt body
- **Don't default to blue** — pick colors that reflect the specific topic
- **Don't mix spacing randomly** — choose 0.3" or 0.5" gaps and use consistently
- **Don't style one slide and leave the rest plain** — commit fully or keep it simple throughout
- **Don't create text-only slides** — add images, icons, charts, or visual elements; avoid plain title + bullets
- **NEVER use accent lines under titles** — these are a hallmark of AI-generated slides; use whitespace or background color instead

### PptxGenJS Correctness
- **NEVER use "#" with hex colors** — causes file corruption in PptxGenJS
- **NEVER encode opacity in hex strings** — use the `opacity` property instead
- **NEVER use async/await in createSlide()** — compile.js won't await
- **NEVER reuse option objects across PptxGenJS calls** — PptxGenJS mutates objects in-place

---

## Critical Pitfalls — PptxGenJS

### NEVER use async/await in createSlide()

```javascript
// WRONG - compile.js won't await
async function createSlide(pres, theme) { ... }

// CORRECT
function createSlide(pres, theme) { ... }
```

### NEVER use "#" with hex colors

```javascript
color: "FF0000"      // CORRECT
color: "#FF0000"     // CORRUPTS FILE
```

### NEVER encode opacity in hex strings

```javascript
shadow: { color: "00000020" }              // CORRUPTS FILE
shadow: { color: "000000", opacity: 0.12 } // CORRECT
```

### Prevent text wrapping in titles

```javascript
// Use fit:'shrink' for long titles
slide.addText("Long Title Here", {
  x: 0.5, y: 2, w: 9, h: 1,
  fontSize: 48, fit: "shrink"
});
```

### NEVER reuse option objects across calls

```javascript
// WRONG
const shadow = { type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 };
slide.addShape(pres.shapes.RECTANGLE, { shadow, ... });
slide.addShape(pres.shapes.RECTANGLE, { shadow, ... });

// CORRECT - factory function
const makeShadow = () => ({ type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 });
slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow(), ... });
slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow(), ... });
```

---