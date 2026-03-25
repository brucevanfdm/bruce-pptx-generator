# QA Checklist & Common Mistakes

For API-level pitfalls (hex color format, reusing option objects, etc.) see [pptxgenjs.md](pptxgenjs.md#common-pitfalls).

---

## Pre-Compile Code Review (Step 5.5)

Run this before compiling. You cannot see rendered output, so catch layout bugs in code now.

Go through every slide JS file and check each item below. **Write down every issue found — do not fix silently.**

### 1. Bounds Check

Slide canvas: **10" wide × 5.625" tall**. Every element must satisfy:

```
x >= 0  AND  x + w <= 10
y >= 0  AND  y + h <= 5.625
```

Common traps:
- Shape at `x:0.5, w:9.8` → right edge = 10.3 ✗ overflows
- Text at `y:5.0, h:0.8` → bottom = 5.8 ✗ overflows
- Page badge at `x:9.3, w:0.4` → right edge = 9.7 ✓

**Flag any element where `x+w > 10` or `y+h > 5.625`.**

### 2. Overlap Check

For each slide, check for unintended overlaps. Two elements overlap when:

```
A.x < B.x+B.w  AND  A.x+A.w > B.x
AND
A.y < B.y+B.h  AND  A.y+A.h > B.y
```

Intentional overlaps (text on a background shape) are fine. Flag these unintended cases:
- Two text boxes at similar x/y that would obscure each other
- A shape covering a text element it shouldn't
- Body content reaching past `y:5.0` (badge lives at `y:5.1`)

### 3. Background Consistency

All slides of the same type must share the exact same background:

| Slide type | Expected background |
|------------|---------------------|
| Cover | One consistent choice for the whole deck |
| TOC | Consistent with Cover or a designated variant |
| Section Divider | **All dividers use the same value** |
| Content pages | **All content pages must be identical** |
| Summary | Matches Cover or a designated closing style |

Common failure: one content slide uses `theme.bg`, another uses `"FFFFFF"` — visually identical now but breaks if the theme changes.

**Fix**: define backgrounds once in `compile.js` and pass them through:

```javascript
const backgrounds = {
  cover:   theme.bg,
  toc:     theme.bg,
  divider: "EEF6FF",
  content: "FFFFFF",   // ALL content pages must use this exact string
  summary: theme.bg,
};
```

### 4. Font Compliance

Scan every `fontFace` value. All should be:
- `"Microsoft YaHei"` — Chinese or mixed content
- The chosen English font (`"Arial"`, `"Georgia"`, etc.)

Flag any unexpected font name.

### 5. Color Compliance

- Every color should come from `theme.*`
- Exceptions allowed: `"FFFFFF"` (white), `"000000"` (black)
- **No `"#"` prefix anywhere** — `"#FF0000"` corrupts the file
- No 8-char hex strings encoding opacity — use the `opacity` property

### 6. Page Badge

Every slide except Cover must have a page badge. Check:
- Badge is present
- Badge shows the correct sequential number
- Position: `x:9.3, y:5.1, w:0.4, h:0.4` (circle) or `x:9.1, y:5.15, w:0.6, h:0.35` (pill)

### 7. Title Structure

For each content / TOC / summary slide:
- Title `y` position is consistent across all content slides (e.g. `y:0.22`)
- Title uses `bold: true` and `color: theme.primary`
- If the style requires an accent bar (e.g. 企业科技蓝 orange line), it is present below the title

### 8. Cross-Slide Consistency Matrix

After individual checks, do one cross-slide pass. Build a table:

| Slide | Type | Title y | fontSize | Content start y | Background |
|-------|------|---------|----------|-----------------|------------|
| 01 | cover | — | — | — | `theme.bg` |
| 02 | toc | 0.22 | 28 | 0.9 | `theme.bg` |
| 03 | divider | — | — | — | `EEF6FF` |
| 04 | content | 0.22 | 28 | 1.05 | `FFFFFF` |
| 05 | content | **0.30** | **26** | 1.05 | `FFFFFF` ← **flag: y and fontSize differ** |

Flag any same-type slides where these values differ.

### How to report findings

```
slide-04.js: shape x:0.5 w:9.8 → right=10.3 → OVERFLOW, change w to 9.5
slide-05.js: background "FFFFFF" but other content slides use theme.bg → INCONSISTENCY
slide-06.js: page badge missing → ADD BADGE
slide-07.js: title y:0.30 but others are y:0.22 → TITLE DRIFT
```

Fix all flagged issues before compiling.

---

## Post-Compile QA

**Assume there are problems. Your job is to find them.**

Your first render is almost never correct. Approach QA as a bug hunt, not a confirmation step.

### Content extraction

```bash
python -m markitdown output.pptx
```

Check for: missing content, wrong order, truncated text.

### Leftover placeholder check

```bash
python -m markitdown output.pptx | grep -iE "xxxx|lorem|ipsum|placeholder|TODO"
```

If this returns results, fix before declaring success.

### Verification loop

1. Compile → extract with markitdown → review content
2. **List issues found** — if none found, look again more critically
3. Fix source JS files → recompile
4. Re-verify affected slides — one fix often creates another problem
5. Repeat until a full pass reveals no new issues

**Do not declare success until you've completed at least one fix-and-verify cycle.**

---

## Common Mistakes to Avoid

### Layout & Positioning

- **Overflow** — always verify `x+w ≤ 10` and `y+h ≤ 5.625`
- **Body reaching badge area** — body content must end by `y:5.0`; badge lives at `y:5.1`
- **Inconsistent backgrounds** — define once in `compile.js`, pass through; don't hardcode per slide
- **Text box default margin** — PptxGenJS adds internal padding; set `margin: 0` when aligning text precisely with shapes
- **Low contrast** — both icons and text need strong contrast against the background
- **Large white space** — use graphic layout components (G1–G5) to fill the content area `y:1.05–5.0`

### Content & Style

- **Repeating the same layout** — vary layout types across slides; use the graphic layout selector in workflow.md
- **Centered body text** — left-align paragraphs and lists; center only titles and KPI numbers
- **Weak size contrast** — titles need 28pt+ to visually separate from 12–14pt body text
- **Single-keyword descriptions** — write complete sentences (2–3 lines per item) so clients understand without a presenter
- **Text-only slides** — add shapes, cards, or visual structure; never plain title + bullet list

### PptxGenJS Correctness

- **`"#"` before hex colors** — causes file corruption; always `"FF0000"` not `"#FF0000"`
- **Opacity in hex strings** — `"00000020"` corrupts; use `{ color: "000000", opacity: 0.12 }`
- **`async` in `createSlide()`** — `compile.js` won't await; always synchronous
- **Reusing option objects** — PptxGenJS mutates objects in-place; use factory functions for shared options like shadows
