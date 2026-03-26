# PPTX Creation Workflow (Steps 1–7)

End-to-end guide for creating a presentation from scratch with PptxGenJS.

---

## Step 1: Research & Requirements

Understand the user's needs before touching any code:
- **Topic** — what is the presentation about?
- **Audience** — who will read it? (client briefing, internal report, investor pitch?)
- **Purpose** — inform, persuade, instruct?
- **Tone** — formal / casual / technical?
- **Content depth** — how much detail per slide? (汇报型 vs 演讲辅助型)
- **Slide count** — rough target

---

## Step 2: Select Style

**如果用户已明确指定风格** → 直接加载对应 preset 文件，跳到 Step 4。

**如果用户没有指定风格** → 用 `AskUserQuestion` 问受众感受，一次提问包含所有信息：

```
Ask questions in ONE AskUserQuestion call:

Question 1 (header: "演讲氛围"):
  受众看完这份演示的感受是什么？
  options:
    - label: "权威可信"
      description: "政企汇报、客户提案、正式场合 → 推荐：企业科技蓝"
    - label: "创新进取"
      description: "产品发布、技术演讲、AI 展示 → 推荐：暗黑科技"
    - label: "简洁高效"
      description: "内部报告、数据汇报、快速同步 → 推荐：简约白"
    - label: "亲切温暖"
      description: "培训课程、HR 沟通、团队分享 → 推荐：暖色商务"

Question 2 (header: "内容深度"):
  每张幻灯片的信息量定位？
  options:
    - label: "客户汇报型（看完即懂）"
      description: "完整语义句，4–7 条，无需现场讲解"
    - label: "演讲辅助型（配合讲解）"
      description: "关键词 + 数字，3–5 条，演讲者补充细节"
```

收到答案后，告知推荐 preset 和理由，然后加载 preset 文件继续。

### Preset 对照表

| Preset | 氛围 | 文件 |
|--------|------|------|
| 企业科技蓝 | 权威、专业、可信 | [default-style.md](default-style.md) |
| 暗黑科技 | 创新、前沿、冲击力 | [dark-tech-style.md](dark-tech-style.md) |
| 简约白 | 克制、专业、数据优先 | [minimal-white-style.md](minimal-white-style.md) |
| 暖色商务 | 亲切、温暖、易接受 | [warm-biz-style.md](warm-biz-style.md) |

When a preset is active:
- Use its `theme` object directly
- Use its provided component functions (`addSlideTitleWithAccent`, `addTOCItem`, `addFeatureItem`, etc.)
- Follow its content density rules
- Its page-type guidance supersedes [custom-style-guide.md](custom-style-guide.md)

**If no preset matches the user's need** → use [custom-style-guide.md](custom-style-guide.md) to build a custom palette.

---

## Step 3: Select Design Style (skip if using a preset)

Use [custom-style-guide.md](custom-style-guide.md) Style Recipes to choose one of:

| Recipe | Feel | Best for |
|--------|------|---------|
| Sharp | Modern, bold, high-contrast | Tech, finance, corporate |
| Soft | Gentle, approachable | Education, healthcare, HR |
| Rounded | Friendly, contemporary | SaaS, startups, consumer |
| Pill | Playful, energetic | Marketing, events, retail |

---

## Step 4: Plan Slide Outline

Classify **every slide** as exactly one of the 5 page types:

| Type | Purpose |
|------|---------|
| Cover | Opening slide — title, subtitle, date/presenter |
| TOC | Table of contents — section overview |
| Section Divider | Chapter break between major sections |
| Content | Main information slides — all variants |
| Summary | Closing — key takeaways, CTA, thank-you |

Ensure visual variety — do NOT use the same content layout on consecutive slides. See [custom-style-guide.md](custom-style-guide.md) for detailed layout options per type (when not using a preset).

---

## Step 4.5: Outline Review (REQUIRED before writing any code)

Fixing problems here is nearly free. Fixing them after generation is expensive.

### Narrative arc check

Does the deck tell a coherent story? Common patterns:
- Client briefing: Problem → Solution → Proof → Action
- Product report: Context → Findings → Analysis → Recommendations
- Training: Background → Concepts → Examples → Summary

If the sequence feels jumpy, reorder now.

### Visual variety map

Write out the slide subtypes in sequence and scan for runs:

```
Bad:  cover → TOC → text → text → text → text → summary
Good: cover → TOC → divider → text → data → divider → comparison → text → summary
```

No more than 2 consecutive content slides with the same subtype.

### Content density balance

Scan each slide's planned content. If any slide has 3× more items than its neighbors, redistribute or split. Dense slides overflow; sparse slides waste space.

### Required structure checklist

- [ ] Deck has a Cover slide
- [ ] If more than 5 slides: TOC is present
- [ ] Each major section has a Section Divider
- [ ] Deck ends with a Summary/Closing slide
- [ ] Total slide count is appropriate for context

Fix any failures before proceeding to Step 5.

---

## Step 5: Generate Slide JS Files

Create one JS file per slide in `slides/`. Each file exports a synchronous `createSlide(pres, theme)` function.

### Graphic Layout Selection (content slides)

Before writing code for each content slide, identify the relationship between its items, then pick the matching layout:

| Content relationship | Layout to use |
|----------------------|---------------|
| Items are parallel / equal / no order | G1 `addParallelCards()` |
| One main concept with sub-items | G2 `addHierarchicalLayout()` |
| Steps with a defined sequence | G3 `addFlowProcess()` |
| Items form a cycle or iterate | G4 `addCycleLayout()` |
| Items have hierarchy / priority levels | G5 `addPyramid()` |
| Numbered feature list | `addFeatureItem()` |
| KPI metrics / data callouts | `addKPICard()` |
| Client pain points / challenge cards | `addInfoCard()` |
| Tabular comparison | `addColumnHeader()` + rows |

All layout functions are defined in the active style preset (e.g. [corporate-tech-blue.md](corporate-tech-blue.md)). Every layout must fill `y: 1.05 – 5.0`; no large white spaces.

### Subagent parallelization

Generate up to 5 slides concurrently using subagents. Tell each subagent:

1. File path: `slides/slide-01.js`, `slides/slide-02.js`, etc.
2. Images: `slides/imgs/`
3. Final PPTX: `slides/output/`
4. Dimensions: 10" × 5.625" (LAYOUT_16x9)
5. Fonts: Chinese = `Microsoft YaHei`, English = `Arial`
6. Colors: 6-char hex without `#`
7. Theme object contract: only 5 keys (`primary`, `secondary`, `accent`, `light`, `bg`)
8. Must follow [pptxgenjs.md](pptxgenjs.md)

### Slide file format

Every slide file must include a DESIGN INTENT block before any code:

```javascript
// slide-03.js
const pptxgen = require("pptxgenjs");

// DESIGN INTENT:
//   Type    : content
//   Layout  : G2 总分布局 — top full-width main concept, bottom 3 sub-cards
//   Focal   : Main box at y:1.05 h:1.1 (dark blue, white text)
//   Zones   : Main box x:0.45–9.55 | Sub-cards 3-col below y:2.65
//   BG      : theme.bg (FFFFFF, same as all content slides)
//   Badge   : slide 03

function createSlide(pres, theme) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // ... slide code here ...

  return slide;
}

// Standalone preview
if (require.main === module) {
  const pres = new pptxgen();
  pres.layout = 'LAYOUT_16x9';
  const theme = {
    primary: "1A3C6E", secondary: "1E88E5", accent: "F5782A",
    light: "E8F4FF", bg: "FFFFFF"
  };
  createSlide(pres, theme);
  pres.writeFile({ fileName: "slide-03-preview.pptx" });
}

module.exports = { createSlide };
```

---

## Step 5.5: Pre-Compile Code Review (REQUIRED)

Review every slide JS file before compiling. Write out findings explicitly — do not silently fix.

Check each slide for:

1. **Bounds** — `x + w ≤ 10` and `y + h ≤ 5.625` for every element
2. **Overlaps** — no unintended collisions between elements
3. **Background consistency** — all content slides use the exact same background value
4. **Font compliance** — only `Microsoft YaHei` and the chosen English font
5. **Color compliance** — only `theme.*` values; no raw hex except `"FFFFFF"` / `"000000"`; no `"#"` prefix
6. **Page badge** — present on every non-cover slide at correct position

See [qa.md](qa.md) for detailed per-check guidance and the cross-slide consistency matrix.

Fix all issues before moving to Step 6.

---

## Step 6: Compile into Final PPTX

Create `slides/compile.js`:

```javascript
// slides/compile.js
const pptxgen = require('pptxgenjs');
const fs = require('fs');
const path = require('path');

const pres = new pptxgen();
pres.layout = 'LAYOUT_16x9';

// ── Theme: replace with the palette chosen in Step 2 ──────────────────────
// Example: 企业科技蓝
const theme = {
  primary:   "1A3C6E",
  secondary: "1E88E5",
  accent:    "F5782A",
  light:     "E8F4FF",
  bg:        "FFFFFF",
};

// ── Auto-discover slide files in order ────────────────────────────────────
const slideFiles = fs.readdirSync(__dirname)
  .filter(f => /^slide-\d+\.js$/.test(f))
  .sort();

for (const file of slideFiles) {
  const mod = require(path.join(__dirname, file));
  mod.createSlide(pres, theme);
}

// ── Output ────────────────────────────────────────────────────────────────
fs.mkdirSync(path.join(__dirname, 'output'), { recursive: true });
pres.writeFile({ fileName: path.join(__dirname, 'output', 'presentation.pptx') });
console.log('Done → slides/output/presentation.pptx');
```

Run with:

```shell
cd slides && node compile.js
```

---

## Step 7: QA (Required)

See [qa.md](qa.md) for the full post-compile QA process.

**Never declare success without completing at least one fix-and-verify cycle.**

---

## Output Structure

```
slides/
├── slide-01.js      # Cover
├── slide-02.js      # TOC
├── slide-03.js      # Section Divider
├── slide-04.js      # Content
├── ...
├── compile.js       # Assembles all slides into PPTX
├── imgs/            # Images referenced by slides
└── output/
    └── presentation.pptx
```
