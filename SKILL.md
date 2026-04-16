---
name: bruce-pptx-generator
description: "Use this skill whenever the user mentions PPT, PPTX, PowerPoint, presentation, slides, or a deck — even casually. Always invoke this skill before generating any slide code or touching any .pptx file."
---
# Bruce 的 PPTX 生成器

## 任务路由

根据任务类型选择正确的路径，然后加载对应文件。

| 任务                               | 加载文件                                                                                                      |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **编辑**现有模板 PPTX        | [editing.md](references/editing.md) + [pptxgenjs.md](references/pptxgenjs.md)                                       |
| **从零创建**（使用风格预设） | [workflow.md](references/workflow.md) + 预设文件 + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md) |

## 风格预设

使用预设时，加载预设文件——其中包含完整的页面布局、组件函数、色板和内容密度规则。

### 风格选择

**如果用户没有指定风格**，默认推荐**华为方案**。如需确认，可用 `AskUserQuestion` 问：受众看完这份演示的感受是什么？

| Preset       | 受众感受 | 字体                | 文件                                                     | 适用场景                                   |
| ------------ | -------- | ------------------- | -------------------------------------------------------- | ------------------------------------------ |
| 麦肯锡蓝     | 逻辑严密 | YaHei + Arial Black | [mckinsey-style.md](references/mckinsey-style.md)           | 战略汇报、咨询报告、管理层提案             |
| 华为方案 | 专业权威 | YaHei + Arial Black | [huawei-style.md](references/huawei-style.md)               | 产品介绍、公司介绍、解决方案、政企客户提案 |
| 苹果极简     | 打动人心 | YaHei + Arial Black | [apple-minimal-style.md](references/apple-minimal-style.md) | 产品发布、Demo、Vision 演讲、对外路演      |
| Pitch Deck   | 卖动     | YaHei + Arial Black | [pitch-deck-style.md](references/pitch-deck-style.md)       | 融资路演、Roadmap 提案、Business Case      |
| 数据分析     | 讲清     | YaHei + Arial Black | [data-analysis-style.md](references/data-analysis-style.md) | 用研汇报、A/B 结果、OKR Review、指标会议   |
| 暗黑科技     | 创新进取 | YaHei + Arial Black | [dark-tech-style.md](references/dark-tech-style.md)         | 产品发布、技术演讲、AI 能力展示            |

告知用户推荐的 preset 并说明理由，然后进入工作流。如果用户不满意，允许手动选择。

## 数据推断原则

**演示文稿中禁止出现模糊表述。** 每个论点必须有具体数字支撑。当用户输入缺乏数据时：

1. **优先追问**：输入中有 1–3 个数据缺口时，用 `AskUserQuestion` 一次性追问所有缺失数字，说明每个数字用在哪张幻灯片。
2. **允许估算**：缺口较多或用户明确说"直接生成"时，使用行业典型基准值，并在幻灯片底部注明「参考行业基准，请替换为实际数据」，且须在回复中告知用户哪些是估算。
3. **严禁空占位**：禁止写"XX%"、"N 个"、"数十万用户"而不填具体数字。

**触发追问的信号词**（出现即追问数字）：
> "很多用户"、"大幅提升"、"显著降低"、"快速增长"、"大量"、"明显"、"有效"

## 精装交付标准（强制）

每份演示文稿必须达到「精装房」标准，禁止交付「标题+一句话」的毛坯房幻灯片。

### 内容富足度（每张内容页必须满足）

1. **数据或统计必须有**：每个核心论点必须搭配一个数字、比例、时间或行业数据支撑。例："慢病随访断档率 > 60%"、"覆盖 1.18 亿空巢老人"。
2. **Tagline 必须有**：每张卡片或每个模块必须有一句 12–20 字的精准定位语，说明「这能解决什么问题」。例："金融级身份认证，数据访问全程可控"。
3. **Bullet 必须带视觉前缀**：使用小方块/小圆点/编号作为前缀，禁止纯文本堆叠。每条 bullet 应为完整语义句，而非单个关键词。
4. **非文字视觉元素必须有**：除苹果极简（Apple Minimal）外，每张内容页至少包含一种非纯文字视觉组件（SVG 图标、数据卡、流程图、进度环、对比矩阵、架构图、KPI 卡）。纯文字列表页视为毛坯房，必须添加视觉元素。苹果极简风格以极简克制为核心，每页视觉元素酌情添加即可。
5. **图形密度上限（防溢出）**：
   - 每张幻灯片最多使用**一种大型图形组件**（流程图 OR 矩阵 OR 进度环组 OR 金字塔，三选一，禁止叠加）
   - 禁止在同一页中同时出现两种大型图形：进度环 + 矩阵、金字塔 + 流程图 = 溢出风险极高
   - 内容区高度仅 3.95"（y:1.05 → y:5.0），大型图形占用后剩余文字空间有限，**添加前必须估算文字是否放得下**
   - **禁止从零手写以下组件**（不在预设库内，需自行实现算法）：漏斗图（funnel）、甘特图（Gantt chart）、雷达图（radar chart）。若当前预设文件中有对应函数则使用预设函数，否则不用。
6. **底部说明/洞察区必须有**：每个核心模块底部应有一句 1–2 行的补充说明，强化价值感或给出行动建议。

### 组件升级原则

每种风格都有对应的**精装 Rich Card 组件**，优先使用，禁止回退到只有 `title + desc` 的基础卡片：

| 风格 | 封面精装 | 内容精装组件 | 禁用的毛坯组件 |
|------|---------|-------------|----------------|
| 华为方案 | `createRichCover` | `addHuaweiRichCard`、`makePainPointCard`、`addHuaweiProcessFlow` | `addHuaweiNumberedCard(title, desc)` |
| 麦肯锡蓝 | `createRichCover` | `addMcKinseyRichCard`、`addIconKpiCard` | `addMcKinseyCard(value, label, desc)` |
| 苹果极简 | `createRichCover` | `addAppleRichCard`、`addAppleKPI` | `addAppleBullets` 单独使用 |
| Pitch Deck | `createRichCover` | `addPitchRichCard`、`addTractionCard` | 纯文字列表页 |
| 暗黑科技 | `createRichCover` | `addDarkRichCard`、`addFeatureItem` | 仅有标题+正文段落 |
| 数据分析 | `createRichCover` | `addDataRichCard`、`createChartWithInsightsSlide` | 纯文字分析页 |

- 封面页必须有装饰性视觉元素（几何图形、SVG 装饰、右侧能力卡片等），禁止只有标题和日期。

## 强制规则

以下规则适用于每份演示文稿的每一张幻灯片。

**尺寸** — 10" × 5.625"（LAYOUT_16x9）。每个元素必须满足 `x + w ≤ 10` 且 `y + h ≤ 5.625`。

**颜色** — 6 位十六进制，不含 `#`（例如 `"FF0000"`）。禁止使用 `"#FF0000"` — 会导致文件损坏。

**字体** — 中文：`Microsoft YaHei` | 英文：`Arial`（或当前预设中指定的替代字体）

**禁用字体** — 以下字体禁止用作展示/标题字体：`宋体`、`仿宋`、`Times New Roman`。在现代演示文稿中会显得业余。

**theme 对象** — 两层约定，必须区分清楚：

**① compile.js / subagent 传入层（严格 5 个键）**

| 键                  | 用途                           |
| ------------------- | ------------------------------ |
| `theme.primary`   | 最深色 — 标题、主要文字       |
| `theme.secondary` | 强调色 — 交互元素、高亮       |
| `theme.accent`    | 标志性点缀色（例如橙色线条）   |
| `theme.light`     | 浅色填充 — 卡片背景、斑马纹行 |
| `theme.bg`        | 幻灯片背景色                   |

compile.js 中定义的 `theme` 对象只传这 5 个键。subagent 在 DESIGN INTENT 注释里也只声明这 5 个。禁止在此层使用：`background`、`text`、`muted`、`darkest`、`lightest` 或其他自造键名。

**② 风格预设文件内部层（允许扩展键）**

各预设文件（`huawei-style.md` 等）中的组件函数（`addHuaweiRichCard`、`makePainPointCard` 等）可以引用预设文件中定义的扩展 key，如 `theme.border`、`theme.bodyText`、`theme.mutedText`、`theme.orangeLight` 等。这些 key 在预设文件的 `theme` const 块中均有定义，不属于违规。

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
