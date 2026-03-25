---
name: bruce-pptx-generator
description: "Use this skill whenever the user mentions PPT, PPTX, PowerPoint, presentation, slides, or a deck — even casually. Handles two scenarios: (1) create a presentation from scratch with PptxGenJS using a complete design system (color palettes, style recipes, 5 slide types); (2) edit an existing PPTX file via XML manipulation. Always invoke this skill before generating any slide code or touching any .pptx file."
license: MIT
metadata:
  version: "2.0"
  category: productivity
  sources:
    - https://gitbrent.github.io/PptxGenJS/
---

# Bruce's PPTX Generator

## Task Routing

Pick the right path based on the task, then load the listed files.

| Task | Load these files |
|------|-----------------|
| **Edit** existing PPTX from template | [editing.md](references/editing.md) + [pptxgenjs.md](references/pptxgenjs.md) |
| **Create from scratch** with style preset | [workflow.md](references/workflow.md) + preset file + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md) |
| **Create from scratch** without preset | [workflow.md](references/workflow.md) + [custom-style-guide.md](references/custom-style-guide.md) + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md) |

## Style Presets

Using a preset? Load the preset file — it contains its own complete page layouts, component functions, color palette, and content density rules. The generic `custom-style-guide.md` is **not needed** when a preset is active.

| Preset | File | Best for |
|--------|------|----------|
| 企业科技蓝（默认） | [default-style.md](references/default-style.md) | AI / 安全 / 产品汇报，政企客户，正式场合，客户汇报型 |

## Reference Files

| File | Purpose |
|------|---------|
| [workflow.md](references/workflow.md) | Steps 1–7 creation workflow, outline review, compile script |
| [pptxgenjs.md](references/pptxgenjs.md) | Complete PptxGenJS API reference |
| [qa.md](references/qa.md) | Pre-compile checklist, post-compile QA, common mistakes |
| [custom-style-guide.md](references/custom-style-guide.md) | Color palettes, style recipes, 5 page types (no preset path only) |
| [editing.md](references/editing.md) | Template-based XML editing workflow |

## Mandatory Rules

These apply to every slide in every presentation.

**Dimensions** — 10" × 5.625" (LAYOUT_16x9). Every element must satisfy `x + w ≤ 10` and `y + h ≤ 5.625`.

**Colors** — 6-char hex without `#` (e.g. `"FF0000"`). Never `"#FF0000"` — causes file corruption.

**Fonts** — Chinese: `Microsoft YaHei` | English: `Arial` (or approved alternative)

**Theme object** — exactly 5 keys, no others:

| Key | Purpose |
|-----|---------|
| `theme.primary` | Darkest color — titles, primary text |
| `theme.secondary` | Accent — interactive elements, highlights |
| `theme.accent` | Signature accent color (e.g. orange line) |
| `theme.light` | Light fill — card backgrounds, zebra rows |
| `theme.bg` | Slide background |

Never use: `background`, `text`, `muted`, `darkest`, `lightest`, or any other key names.

**Page badge** — required on every slide except the Cover:
- Circle: `x: 9.3, y: 5.1, w: 0.4, h: 0.4`
- Pill: `x: 9.1, y: 5.15, w: 0.6, h: 0.35`
- Show page number only (e.g. `"3"`), never `"3/12"`

**`createSlide()` must be synchronous** — never `async`. compile.js won't await it.

## Dependencies

```shell
npm install -g pptxgenjs
```
