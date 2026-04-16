---
name: bruce-pptx-generator
description: "Use this skill when the user explicitly wants to create, generate, export, compile, edit, revise, or restructure a PowerPoint / PPT / PPTX / slide deck artifact. Trigger when the request clearly targets slides, a deck, or a .ppt/.pptx file as the output or editing target, including Chinese equivalents such as 幻灯片、演示文稿、PPT、PPTX、路演 deck. Do not trigger for generic proposal writing, solution discussion, presentation speaking notes, or status-update wording unless the user is explicitly asking for slide files or deck generation."
---
# Bruce 的 PPTX 生成器

## 任务路由

先判断用户要的到底是**生成新 deck**还是**编辑现有 deck**。两条路径的约束不同，不可混用。

### 路由原则

- **生成路径**：用户明确要从零创建、生成、导出、编译新的 PPT / PPTX / slide deck。
- **编辑路径**：用户已经提供或明确指定现有 `.ppt` / `.pptx` 文件，目标是替换内容、重排结构、删改页面或保留模板风格做更新。
- **不要误触发**：如果用户只是写提案、整理汇报思路、润色演讲稿、讨论 presentation 内容，但没有要求生成或编辑幻灯片文件，不使用本 skill。

| 任务                               | 加载文件                                                                                                      |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **编辑**现有模板 PPTX        | [editing.md](references/editing.md) + [pptxgenjs.md](references/pptxgenjs.md)                                       |
| **从零创建**（使用风格预设） | [workflow.md](references/workflow.md) + 预设文件 + [pptxgenjs.md](references/pptxgenjs.md) + [qa.md](references/qa.md) |

### 路由隔离

- **仅在生成路径**下使用 `createSlide()`、`compile.js`、`theme` 五键约定、页码徽章、Rich Card 组件和封面/目录/章节分隔页规则。
- **编辑路径**默认保留模板结构和视觉语言，除非用户明确要求“整套重建为代码生成版”，否则不要把生成路径的组件规范硬套到 XML 编辑任务上。
- **编辑路径**的首要目标是模板兼容、最小必要改动和重新打包后的文件可打开；**生成路径**的首要目标是新 deck 的叙事、布局和一致性。

## 执行环境与回退

- 优先使用运行环境里可用的**结构化提问工具**来一次性收集风格或缺失数据；如果没有该工具，就直接在对话里一次性提问全部必要信息。
- 优先使用运行环境里可用的**精确编辑工具**修改 XML 或代码；如果没有同名工具，使用当前平台提供的等价精确编辑能力。避免依赖批量替换脚本。
- 文中的命令以流程说明为主，按当前 shell 选择等价写法。Windows PowerShell、bash、zsh 可使用各自原生命令，只要行为一致即可。

## 风格预设

使用预设时，加载预设文件——其中包含完整的页面布局、组件函数、色板和内容密度规则。

### 风格选择

**如果用户没有指定风格**，优先用结构化提问工具询问受众感受（见 workflow.md §2）；如果没有该工具，就直接在对话中一次性提问。默认推荐选项为**华为方案（专业权威）**。

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

1. **优先追问**：输入中有 1–3 个数据缺口时，优先使用结构化提问工具；若不可用，就在一次消息中追问所有缺失数字，并说明每个数字用在哪张幻灯片。
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
| 华为方案 | `createRichCover` | `addHuaweiRichCard`、`makePainPointCard`、`addHuaweiProcessFlow` | `addHuaweiNumberedCard` 的基础用法（仅传 title+desc，无 tagline/bullet/底部说明） |
| 麦肯锡蓝 | `createRichCover` | `addMcKinseyRichCard`、`makeProgressRing` + KPI 卡 | `addMcKinseyCard(value, label, desc)` |
| 苹果极简 | `createRichCover` | `addAppleRichCard`、`addAppleKPI` | `addAppleBullets` 单独使用 |
| Pitch Deck | `createRichCover` | `addPitchRichCard`、`addTractionCard` | 纯文字列表页 |
| 暗黑科技 | `createRichCover` | `addDarkRichCard`、`addFeatureItem` | 仅有标题+正文段落 |
| 数据分析 | `createRichCover` | `addDataRichCard`、`createChartWithInsightsSlide` | 纯文字分析页 |

- 封面页必须有装饰性视觉元素（几何图形、SVG 装饰、右侧能力卡片等），禁止只有标题和日期。
- **注意**：`createRichCover` 在各风格中参数签名不同（华为版有 `metrics`/`valueSlogan`，苹果版有 `spotlight`，Pitch Deck 版有 `traction`/`stage`），使用前必须查阅当前预设文件的调用示例，不可跨风格套用参数。

## 强制规则

以下规则**仅适用于从零代码生成路径**，以及用户明确要求按 PptxGenJS 重新生成幻灯片的任务。编辑现有模板时，以模板兼容性、内容适配和最小必要结构改动为准。

**尺寸** — 10" × 5.625"（LAYOUT_16x9）。每个元素必须满足 `x + w ≤ 10` 且 `y + h ≤ 5.625`。

**颜色** — 6 位十六进制，不含 `#`（例如 `"FF0000"`）。禁止使用 `"#FF0000"` — 会导致文件损坏。

**字体** — 中文：`Microsoft YaHei` | 英文：`Arial`（或当前预设中指定的替代字体）

**禁用字体** — 以下字体禁止用作展示/标题字体：`宋体`、`仿宋`、`Times New Roman`。在现代演示文稿中会显得业余。

**theme 对象** — 仅在生成路径中使用，两层约定必须区分清楚：

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

**页码徽章** — 仅适用于生成路径。除封面外每张幻灯片都必须有。只显示页码数字（例如 `"3"`），禁止使用 `"3/12"` 格式。具体坐标和形状以当前预设文件中的 `addPageBadge` 实现为准（qa.md §6 有各预设的参考值）。

**`createSlide()` 必须是同步函数** — 仅适用于生成路径，禁止使用 `async`。compile.js 不会 await 它。

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
- `#` 前缀颜色值（`"#1F3864"` → 改为 `"1F3864"`）— 会导致文件损坏

## 依赖安装

先检查依赖是否已可用；**缺失时再安装**。不要默认每次都重复安装。

**必需依赖（生成或编译前确保可用）：**

```shell
npm install -g pptxgenjs
```

**按需依赖（仅在使用对应功能时）：**

```shell
# 使用 react-icons 图标时（workflow.md 步骤 4.8）
npm install -g react-icons react react-dom sharp

# 编译后内容提取与 QA 验证时（qa.md 编译后 QA 章节）
pip install markitdown
```
