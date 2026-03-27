---
name: bruce-pptx-generator
description: "Use this skill whenever the user mentions PPT, PPTX, PowerPoint, presentation, slides, or a deck — even casually. Handles two scenarios: (1) create a presentation from scratch with PptxGenJS using a complete design system (color palettes, style recipes, 5 slide types); (2) edit an existing PPTX file via XML manipulation. Always invoke this skill before generating any slide code or touching any .pptx file."
license: MIT
metadata:
  version: "4.0"
  category: productivity
  sources:
    - https://gitbrent.github.io/PptxGenJS/
---
# Bruce's PPTX Generator

## Task Routing

Pick the right path based on the task, then load the listed files.

| Task                                            | Load these files                                                                                                                                            |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Edit** existing PPTX from template      | [editing.md](references/editing.md) + [pptxgenjs.md](references/pptxgenjs.md)                                                                                     |
| **Create from scratch** with style preset | [workflow.md](references/workflow.md) + preset file + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md)                                            |
| **Create from scratch** without preset    | [workflow.md](references/workflow.md) + [custom-style-guide.md](references/custom-style-guide.md) + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md) |

## Style Presets

Using a preset? Load the preset file — it contains its own complete page layouts, component functions, color palette, and content density rules. The generic `custom-style-guide.md` is **not needed** when a preset is active.

### 风格选择流程

**如果用户没有指定风格**，默认推荐**麦肯锡蓝**（最常用风格）。如需确认，可用 `AskUserQuestion` 问受众感受：

Ask (header: "演讲氛围"):
> 受众看完这份演示的感受是什么？

| 选项 | description | 推荐 preset |
| ---- | ----------- | ----------- |
| 逻辑严密 | 战略汇报、咨询报告、管理层提案 | **麦肯锡蓝**（默认） |
| 权威可信 | 政企汇报、客户提案、正式场合 | 企业科技蓝 |
| 创新进取 | 产品发布、技术演讲、AI 展示 | 暗黑科技 |
| 简洁高效 | 内部报告、数据汇报、快速同步 | 简约白 |
| 亲切温暖 | 培训课程、HR 沟通、团队分享 | 暖色商务 |

告知用户推荐的 preset 并说明理由，然后进入工作流。如果用户不满意，允许手动选择。

### Preset 列表

| Preset | 氛围 | 字体组合 | 文件 | Best for |
| ------ | ---- | -------- | ---- | -------- |
| **麦肯锡蓝**（默认） | 权威、逻辑、顾问感 | Microsoft YaHei + Arial Black | [mckinsey-style.md](references/mckinsey-style.md) | 战略汇报、咨询报告、管理层提案、年度规划 |
| 企业科技蓝 | 权威、专业、可信 | Microsoft YaHei + Arial | [default-style.md](references/default-style.md) | AI / 安全 / 产品汇报，政企客户，正式场合 |
| 暗黑科技 | 创新、前沿、冲击力 | Microsoft YaHei + Arial Black | [dark-tech-style.md](references/dark-tech-style.md) | 产品发布、技术演讲、AI 能力展示 |
| 简约白 | 克制、专业、数据优先 | Microsoft YaHei + Arial | [minimal-white-style.md](references/minimal-white-style.md) | 内部报告、数据汇报、投资人 Deck |
| 暖色商务 | 亲切、温暖、易接受 | Microsoft YaHei + Arial | [warm-biz-style.md](references/warm-biz-style.md) | 培训课程、HR 沟通、企业文化分享 |

## Reference Files

| File                                                   | Purpose                                                           |
| ------------------------------------------------------ | ----------------------------------------------------------------- |
| [workflow.md](references/workflow.md)                     | Steps 1–7 creation workflow, outline review, compile script      |
| [pptxgenjs.md](references/pptxgenjs.md)                   | Complete PptxGenJS API reference                                  |
| [qa.md](references/qa.md)                                 | Pre-compile checklist, post-compile QA, common mistakes           |
| [mckinsey-style.md](references/mckinsey-style.md)         | 麦肯锡蓝 preset：深蓝标题栏、Action Title、MECE 原则（默认风格） |
| [custom-style-guide.md](references/custom-style-guide.md) | Color palettes, style recipes, 5 page types (no preset path only) |
| [editing.md](references/editing.md)                       | Template-based XML editing workflow                               |

## Mandatory Rules

These apply to every slide in every presentation.

**Dimensions** — 10" × 5.625" (LAYOUT_16x9). Every element must satisfy `x + w ≤ 10` and `y + h ≤ 5.625`.

**Colors** — 6-char hex without `#` (e.g. `"FF0000"`). Never `"#FF0000"` — causes file corruption.

**Fonts** — Chinese: `Microsoft YaHei` | English: `Arial` (or the approved alternative specified in the active preset)

**Font anti-patterns** — Never use as display/title font: `宋体`, `仿宋`, `Times New Roman`. These read as amateur in modern presentations.

**Theme object** — exactly 5 keys, no others:

| Key                 | Purpose                                    |
| ------------------- | ------------------------------------------ |
| `theme.primary`   | Darkest color — titles, primary text      |
| `theme.secondary` | Accent — interactive elements, highlights |
| `theme.accent`    | Signature accent color (e.g. orange line)  |
| `theme.light`     | Light fill — card backgrounds, zebra rows |
| `theme.bg`        | Slide background                           |

Never use: `background`, `text`, `muted`, `darkest`, `lightest`, or any other key names.

**Page badge** — required on every slide except the Cover:

- Circle: `x: 9.3, y: 5.1, w: 0.4, h: 0.4`
- Pill: `x: 9.1, y: 5.15, w: 0.6, h: 0.35`
- Show page number only (e.g. `"3"`), never `"3/12"`

**`createSlide()` must be synchronous** — never `async`. compile.js won't await it.

## DO NOT (常见 AI 生成质量陷阱)

这些是最容易让演示文稿显得低质量的模式，每次生成都要主动避免：

**内容密度**
- 单张 content slide 超过 6 个 bullet point — 超出就拆成两张
- 每条 bullet 超过 20 个字 — 精简或改用卡片布局
- 连续 3 张以上相同布局类型

**视觉**
- 各 slide 背景色不一致（content slide 必须统一用 `theme.bg`）
- 每个元素都加渐变色 — 渐变只用于强调，不滥用
- 所有内容居中对齐 — 会显得呆板，左对齐更有层次感
- 装饰性色块堆砌，没有布局逻辑

**文字**
- 标题照抄正文第一句 — 标题应该是结论或主旨，不是描述
- 英文 text 混用宋体/仿宋 — 英文必须用指定英文字体
- `#` 前缀颜色值（`"#1A3C6E"` → 改为 `"1A3C6E"`）— 会导致文件损坏

## Dependencies

```shell
npm install -g pptxgenjs
```
