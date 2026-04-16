# PPTX 制作流程（第 1–7 步）

使用 PptxGenJS 从零开始创建演示文稿的完整指南。

## 第 1 步：调研与需求确认

在动手写代码之前，先理解用户的需求：
- **主题** — 演示文稿讲的是什么？
- **受众** — 谁来看？（客户汇报、内部报告、投资人路演？）
- **目的** — 告知、说服，还是培训？
- **语气** — 正式 / 轻松 / 技术性？
- **内容深度** — 每张幻灯片的信息量？（汇报型 vs 演讲辅助型）
- **幻灯片数量** — 大致目标

## 第 2 步：选择风格

**如果用户已明确指定风格** → 直接加载对应 preset 文件，跳到第 4 步。

**如果用户没有指定风格** → 用 `AskUserQuestion` 问受众感受，一次提问包含所有信息：

```
在一次 AskUserQuestion 调用中提问所有问题：

问题 1（标题："演讲氛围"）：
  受众看完这份演示的感受是什么？
  options:
    - label: "逻辑严密"
      description: "战略汇报、咨询报告、管理层提案 → 推荐：麦肯锡蓝"
    - label: "打动人心"
      description: "产品发布、Demo、Vision 演讲、对外路演 → 推荐：苹果极简"
    - label: "卖动"
      description: "融资路演、Roadmap 提案、Business Case → 推荐：Pitch Deck"
    - label: "讲清"
      description: "用研汇报、A/B 结果、OKR Review、指标会议 → 推荐：数据分析"
    - label: "创新进取"
      description: "产品发布、技术演讲、AI 能力展示 → 推荐：暗黑科技"

问题 2（标题："内容深度"）：
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
| 麦肯锡蓝 | 逻辑、权威、顾问感 | [mckinsey-style.md](mckinsey-style.md) |
| 苹果极简 | 打动人心、视觉叙事 | [apple-minimal-style.md](apple-minimal-style.md) |
| Pitch Deck | 卖动、说服、路演 | [pitch-deck-style.md](pitch-deck-style.md) |
| 数据分析 | 讲清、数据优先 | [data-analysis-style.md](data-analysis-style.md) |
| 暗黑科技 | 创新、前沿、冲击力 | [dark-tech-style.md](dark-tech-style.md) |

当某个 preset 生效时：
- 直接使用其 `theme` 对象
- 使用其提供的组件函数（各 preset 文件中定义）
- 遵循其内容密度规则和 5 种页面类型

## 第 3 步：生成大纲并获取用户确认

**在写任何代码之前，先生成可见大纲并等待用户确认。** 大纲是整个演示文稿的执行合同——确认后各 subagent 按合同执行，不再自行发挥内容和结构。

### 3.1 选择故事弧线模板

根据演示目的从以下模板选择，或自由组合：

| 模板 | 适用场景 | 标准弧线（可按需增减节点） |
|------|---------|--------------------------|
| **解决方案** | 产品/方案汇报、政企提案 | 行业痛点 → 市场规模 → 解决方案全景 → 核心能力 → 案例证明 → ROI/价值 → 下一步 |
| **管理汇报** | 战略汇报、OKR、执委会 | 核心结论 → 现状数据 → 问题分解 → 方案选项 → 推荐方案 → 落地计划 → 资源需求 |
| **融资路演** | 投资人 Pitch、融资路演 | 问题 → 解法 → 市场规模 → 产品 → 牵引力/数据 → 团队 → 融资需求 & 用途 |
| **数据汇报** | 用研结论、A/B、OKR Review | 核心发现 → 背景 → 数据维度 1 → 维度 2 → 维度 3 → 综合洞察 → 行动建议 |

### 3.2 生成大纲表格

以结构化表格呈现每张幻灯片，同步暴露所有数据缺口：

> **组件名称来源**：大纲表格中的组件名（`createRichCover`、`createTOCSlide`、`makePainPointCard` 等）均为当前加载的预设文件中定义的函数。**禁止自行实现**——确认预设文件已加载后再填写组件列。

| # | 类型 | 标题（结论句） | 核心组件 | ⚠️ 待补充 |
|---|------|--------------|---------|----------|
| 01 | Cover | [演示标题] | `createRichCover`（签名因风格而异，见预设文件调用示例） | — |
| 02 | TOC | 目录 | `createTOCSlide` | — |
| 03 | Section | 一、[章节名] | `createSectionDivider` | — |
| 04 | Content | [含具体数字的结论句] | `makePainPointCard × 3` | ⚠️ [缺失数字] |
| 05 | Content | [含具体数字的结论句] | `addHuaweiRichCard × 3` | — |
| N | Summary | [行动号召句] | `createSummarySlide` | — |

**大纲表格强制规则：**

- **标题列** — 必须是结论句/价值句，含具体数字优先。❌ "产品功能介绍" → ✅ "三大核心能力将交付周期压缩 40%"
- **核心组件列** — 具体到函数名。❌ "卡片布局" → ✅ `addHuaweiRichCard × 3`
- **⚠️ 待补充列** — 所有尚未获得的具体数字、比例、时间节点，全部列出

### 3.3 数据缺口处理（确认前必须解决）

大纲中每个 `⚠️` 项，**必须通过以下一种方式解决后才能推进**：

**方式 A — 追问用户**（推荐，适合 1–3 个数据缺口）
用 `AskUserQuestion` 一次性提问所有缺失数据点，说明每个数字用在哪张幻灯片。

**方式 B — 行业基准估算**（缺口较多或用户授权时）
使用典型行业基准值，并在幻灯片底部注明「参考行业基准，请替换为实际数据」，同时在回复中告知用户哪些是估算。

**严格禁止：**
- 幻灯片中出现"大幅"、"显著"、"很多"、"明显提升"等无量词的模糊表述
- 使用"XX%"、"N 个"、"数十万"等空位符而不填入真实或估算数字
- 为避免麻烦而直接生成占位数字但不告知用户

### 3.4 等待用户确认

输出大纲表格后**暂停并等待用户反馈**。用户可以：
- 调整幻灯片数量、顺序、标题措辞
- 补充 `⚠️` 项的数据
- 直接说"可以"或"开始"

**收到用户确认后才进入第 4 步。禁止在用户未确认大纲前写任何幻灯片代码。**

## 第 4 步：规划幻灯片大纲（内部实现规划，不修改第 3 步确认的内容）

> **注意**：第 3 步已与用户确认了幻灯片列表和组件选择。本步骤只做实现层面的规划（函数调用细节、坐标区域划分），禁止修改幻灯片数量、顺序或标题措辞。

将**每张幻灯片**精确归类为以下 5 种页面类型之一：

| 类型 | 用途 |
|------|---------|
| Cover | 开场幻灯片 — 标题、副标题、日期/演讲者 |
| TOC | 目录 — 章节概览 |
| Section Divider | 主要章节之间的分隔页 |
| Content | 主要内容幻灯片 — 所有变体 |
| Summary | 结尾 — 关键要点、行动号召、致谢 |

确保视觉多样性 — 不要在连续幻灯片中使用相同的内容布局。各类型的详细布局选项请参阅当前 preset 文件的"5 种页面类型"章节。

## 第 4.5 步：大纲审查（写代码前必须完成）

在此阶段修复问题几乎零成本，生成后再修复代价高昂。

### 叙事弧线检查

整个 deck 是否讲述了一个连贯的故事？常见模式：
- 客户汇报：问题 → 解决方案 → 证明 → 行动
- 产品报告：背景 → 发现 → 分析 → 建议
- 培训：背景 → 概念 → 示例 → 总结

如果顺序感觉跳跃，现在就调整。

### 视觉多样性映射

按顺序列出幻灯片子类型，检查是否有连续重复：

```
差：  cover → TOC → text → text → text → text → summary
好：  cover → TOC → divider → text → data → divider → comparison → text → summary
```

相同子类型的内容幻灯片不得连续超过 2 张。

### 内容密度平衡

扫描每张幻灯片的计划内容。如果某张幻灯片的条目是相邻幻灯片的 3 倍，应重新分配或拆分。密度过高的幻灯片会溢出，密度过低的幻灯片浪费空间。

### 必要结构检查清单

- [ ] deck 有封面幻灯片
- [ ] 超过 5 张幻灯片时：包含目录
- [ ] 每个主要章节有章节分隔页
- [ ] deck 以总结/结尾幻灯片收尾
- [ ] 幻灯片总数与场景相符

进入第 5 步前修复所有不符合项。

## 第 4.8 步：初始化工具文件（需要 react-icons 图标时）

如果演示文稿中有任何通过 `iconToBase64Png` 使用 react-icons 图标的调用，在开始写 slide 文件之前，先在 `slides/` 目录创建以下工具文件。只需创建一次。

```javascript
// slides/icon-utils.js
const React = require("react");
const { renderToStaticMarkup } = require("react-dom/server");
const sharp = require("sharp");

async function iconToBase64Png(IconComponent, color, size = 256) {
  const svg = renderToStaticMarkup(
    React.createElement(IconComponent, { color, size })
  );
  const pngBuf = await sharp(Buffer.from(svg)).resize(size, size).png().toBuffer();
  return "image/png;base64," + pngBuf.toString("base64");
}

module.exports = { iconToBase64Png };
```

安装依赖（全局，只需执行一次）：
```shell
npm install -g react-icons react react-dom sharp
```

使用图标时，**compile.js 整个文件必须包裹在 `(async () => { ... })()` 中**，因为 CommonJS 不支持顶层 `await`。完整写法见 mckinsey-style.md § 8 的 compile.js 示例。

## 第 5 步：生成幻灯片 JS 文件

在 `slides/` 中为每张幻灯片创建一个 JS 文件，每个文件导出一个同步的 `createSlide(pres, theme)` 函数。

### 图形布局选择（内容幻灯片）

为每张内容幻灯片写代码前，先确定其条目之间的关系，再从 preset 的"5 种页面类型 → Content"章节中选择匹配的布局：

| 内容关系 | 布局方向 |
|----------------------|---------------|
| 条目并列 / 平等 / 无顺序 | 横排卡片或多列布局 |
| 一个主概念 + 若干子条目 | 顶部全宽主框 + 底部子卡片 |
| 有明确顺序的步骤 | 横向流程箭头 / 时间轴 SVG |
| KPI 指标 / 数据标注 | 横排 KPI 卡，大数字居中 |
| 表格对比 | 表格行列，斑马行 |
| 痛点/场景描述 | 带图标 + 数据标签的痛点卡片矩阵 |

**视觉富足要求**：
- 除苹果极简风格外，每张内容页至少使用一种非纯文字视觉元素（SVG 图标、流程图、进度环、对比矩阵、KPI 卡、时间轴、金字塔等）
- 封面页必须包含装饰性几何图形或右侧能力矩阵卡片
- 优先使用预设中的**精装组件**（`addHuaweiRichCard`、`addHuaweiProcessFlow`、`makePainPointCard`、`addHuaweiKpiCard`），避免仅使用最基础的 `addHuaweiNumberedCard(title, desc)`
- **每张幻灯片最多使用一种大型图形组件**（流程图 OR 进度环组 OR 矩阵 OR 金字塔，禁止在同一页叠加两种大型图形，内容区只有 3.95"，叠加必定溢出）
- **大型图形添加前必须估算剩余文字空间**：内容区高度 3.95"，大型图形占用后剩余高度必须足够放下所有文字（见 qa.md § 1.5 文字溢出估算）

每个布局必须填满 `y: 1.05 – 5.0`，不留大面积空白。

### subagents 并行化

使用 subagents 并行生成最多 5 张幻灯片。告知每个 subagent：

1. 文件路径：`slides/slide-01.js`、`slides/slide-02.js` 等
2. 图片目录：`slides/imgs/`
3. 最终 PPTX：`slides/output/`
4. 尺寸：10" × 5.625"（LAYOUT_16x9）
5. 字体：中文 = `Microsoft YaHei`，英文 = `Arial`
6. 颜色：6 位十六进制，不带 `#`
7. theme 对象约定：仅 5 个键（`primary`、`secondary`、`accent`、`light`、`bg`）
8. **必须遵循精装交付标准**：每张内容页必须包含数据/统计、tagline、bullet 前缀、至少一种非文字视觉元素（SVG 图标/流程图/对比矩阵）、底部说明区
9. 必须遵循 [pptxgenjs.md](pptxgenjs.md)

### 内容富足检查清单（第 5.3 步）

所有幻灯片 JS 文件生成完成后、编译前，执行 [qa.md 第 0 步「内容富足度检查」](qa.md) — 6 项全部通过方可进入编译。任何一项未通过，返回对应幻灯片修改后重检。

### 幻灯片文件格式

每个幻灯片文件必须在代码前包含 DESIGN INTENT 块：

```javascript
// slide-03.js
const pptxgen = require("pptxgenjs");

// DESIGN INTENT:
//   类型    : content（内容页）
//   布局  : G2 总分布局 — 顶部全宽主概念，底部 3 个子卡片
//   焦点   : 主框在 y:1.05 h:1.1（深蓝色，白色文字）
//   区域   : 主框 x:0.45–9.55 | 子卡片 3 列，位于 y:2.65 以下
//   背景      : theme.bg（FFFFFF，与所有内容页一致）
//   页码标记   : slide 03

function createSlide(pres, theme) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // ... 幻灯片代码 ...

  return slide;
}

// 独立预览
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

## 第 5.5 步：编译前代码审查（必须完成）

编译前审查每个幻灯片 JS 文件。明确写出发现的问题，不要悄悄修复。

逐张幻灯片检查：

1. **边界** — 每个元素满足 `x + w ≤ 10` 且 `y + h ≤ 5.625`
2. **重叠** — 元素之间无非预期碰撞
3. **背景一致性** — 所有内容幻灯片使用完全相同的背景值
4. **字体合规** — 仅使用 `Microsoft YaHei` 和所选英文字体
5. **颜色合规** — 仅使用 `theme.*` 值；除 `"FFFFFF"` / `"000000"` 外不使用原始十六进制；不带 `"#"` 前缀
6. **页码标记** — 每张非封面幻灯片的正确位置均有页码标记

详细的逐项检查指南和跨幻灯片一致性矩阵请参阅 [qa.md](qa.md)。

进入第 6 步前修复所有问题。

## 第 6 步：编译为最终 PPTX

创建 `slides/compile.js`：

```javascript
// slides/compile.js
const pptxgen = require('pptxgenjs');
const fs = require('fs');
const path = require('path');

const pres = new pptxgen();
pres.layout = 'LAYOUT_16x9';

// ── 主题：替换为第 2 步选定的调色板 ──────────────────────
// 示例：企业科技蓝
const theme = {
  primary:   "1A3C6E",
  secondary: "1E88E5",
  accent:    "F5782A",
  light:     "E8F4FF",
  bg:        "FFFFFF",
};

// ── 按顺序自动发现幻灯片文件 ────────────────────────────────────
const slideFiles = fs.readdirSync(__dirname)
  .filter(f => /^slide-\d+\.js$/.test(f))
  .sort();

for (const file of slideFiles) {
  const mod = require(path.join(__dirname, file));
  mod.createSlide(pres, theme);
}

// ── 输出 ────────────────────────────────────────────────────────────────
fs.mkdirSync(path.join(__dirname, 'output'), { recursive: true });
pres.writeFile({ fileName: path.join(__dirname, 'output', 'presentation.pptx') });
console.log('Done → slides/output/presentation.pptx');
```

运行命令：

```shell
cd slides && node compile.js
```

## 第 7 步：质量检查（必须完成）

完整的编译后质量检查流程请参阅 [qa.md](qa.md)。

**在完成至少一轮修复并验证之前，不得宣布成功。**

## 输出结构

```
slides/
├── slide-01.js      # 封面
├── slide-02.js      # 目录
├── slide-03.js      # 章节分隔页
├── slide-04.js      # 内容页
├── ...
├── compile.js       # 将所有幻灯片组合为 PPTX
├── imgs/            # 幻灯片引用的图片
└── output/
    └── presentation.pptx
```
