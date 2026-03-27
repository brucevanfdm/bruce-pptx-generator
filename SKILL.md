---
name: bruce-pptx-generator
description: "Use this skill whenever the user mentions PPT, PPTX, PowerPoint, presentation, slides, or a deck — even casually. Always invoke this skill before generating any slide code or touching any .pptx file."
---
# Bruce 的 PPTX 生成器

## 任务路由

根据任务类型选择正确的路径，然后加载对应文件。

| 任务                                        | 加载文件                                                                                                                                                    |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **编辑**现有模板 PPTX               | [editing.md](references/editing.md) + [pptxgenjs.md](references/pptxgenjs.md)                                                                                     |
| **从零创建**（使用风格预设）       | [workflow.md](references/workflow.md) + 预设文件 + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md) |

## 风格预设

使用预设时，加载预设文件——其中包含完整的页面布局、组件函数、色板和内容密度规则。

### 风格选择

**如果用户没有指定风格**，默认推荐**麦肯锡蓝**。如需确认，可用 `AskUserQuestion` 问：受众看完这份演示的感受是什么？

| Preset | 受众感受 | 字体 | 文件 | 适用场景 |
| ------ | -------- | ---- | ---- | -------- |
| **麦肯锡蓝**（默认） | 逻辑严密 | YaHei + Arial Black | [mckinsey-style.md](references/mckinsey-style.md) | 战略汇报、咨询报告、管理层提案 |
| 苹果极简 | 打动人心 | YaHei + Arial Black | [apple-minimal-style.md](references/apple-minimal-style.md) | 产品发布、Demo、Vision 演讲、对外路演 |
| Pitch Deck | 卖动 | YaHei + Arial Black | [pitch-deck-style.md](references/pitch-deck-style.md) | 融资路演、Roadmap 提案、Business Case |
| 数据分析 | 讲清 | YaHei + Arial Black | [data-analysis-style.md](references/data-analysis-style.md) | 用研汇报、A/B 结果、OKR Review、指标会议 |
| 暗黑科技 | 创新进取 | YaHei + Arial Black | [dark-tech-style.md](references/dark-tech-style.md) | 产品发布、技术演讲、AI 能力展示 |

告知用户推荐的 preset 并说明理由，然后进入工作流。如果用户不满意，允许手动选择。

## 强制规则

以下规则适用于每份演示文稿的每一张幻灯片。

**尺寸** — 10" × 5.625"（LAYOUT_16x9）。每个元素必须满足 `x + w ≤ 10` 且 `y + h ≤ 5.625`。

**颜色** — 6 位十六进制，不含 `#`（例如 `"FF0000"`）。禁止使用 `"#FF0000"` — 会导致文件损坏。

**字体** — 中文：`Microsoft YaHei` | 英文：`Arial`（或当前预设中指定的替代字体）

**禁用字体** — 以下字体禁止用作展示/标题字体：`宋体`、`仿宋`、`Times New Roman`。在现代演示文稿中会显得业余。

**theme 对象** — 恰好 5 个键，不多不少：

| 键                  | 用途                                       |
| ------------------- | ------------------------------------------ |
| `theme.primary`   | 最深色 — 标题、主要文字                   |
| `theme.secondary` | 强调色 — 交互元素、高亮                   |
| `theme.accent`    | 标志性点缀色（例如橙色线条）               |
| `theme.light`     | 浅色填充 — 卡片背景、斑马纹行             |
| `theme.bg`        | 幻灯片背景色                               |

禁止使用：`background`、`text`、`muted`、`darkest`、`lightest` 或其他任何键名。

**页码徽章** — 除封面外每张幻灯片都必须有：

- 圆形：`x: 9.3, y: 5.1, w: 0.4, h: 0.4`
- 胶囊形：`x: 9.1, y: 5.15, w: 0.6, h: 0.35`
- 只显示页码数字（例如 `"3"`），禁止使用 `"3/12"` 格式

**`createSlide()` 必须是同步函数** — 禁止使用 `async`。compile.js 不会 await 它。

## 禁止事项（常见 AI 生成质量陷阱）

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

## 依赖安装

```shell
npm install -g pptxgenjs
```
