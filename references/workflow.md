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

**如果用户没有指定风格** → 优先使用结构化提问工具，一次性收集受众感受和内容深度；如果运行环境没有该工具，就直接在对话里一次性提问。**华为方案**是默认推荐选项，在选项描述中已标注"（默认）"：

```
在一次结构化提问中收集所有问题；若没有结构化提问工具，就把下面两题合并成一条消息发送给用户：

问题 1（标题："演讲氛围"）：
  受众看完这份演示的感受是什么？
  options:
    - label: "专业权威"
      description: "产品介绍、公司介绍、解决方案、政企客户提案 → 推荐：华为方案（默认）"
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
| 华为方案（默认） | 专业权威、解决方案感 | [huawei-style.md](huawei-style.md) |
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
>
> **新增要求**：大纲在确认时就要暴露 deck skeleton，包括 `Section` 和 `Master`。不要等到写代码时才临时决定骨架。

| # | 类型 | Section | 标题（结论句） | Master | 核心组件 | ⚠️ 待补充 |
|---|------|---------|--------------|--------|---------|----------|
| 01 | Cover | — | [演示标题] | `COVER_MASTER` | `createRichCover`（签名因风格而异，见预设文件调用示例） | — |
| 02 | TOC | — | 目录 | `TOC_MASTER` | `createTOCSlide` | — |
| 03 | Section | 市场机会 | 一、市场机会 | `SECTION_MASTER` | `createSectionDivider` | — |
| 04 | Content | 市场机会 | [含具体数字的结论句] | `CONTENT_MASTER` | `makePainPointCard × 3` | ⚠️ [缺失数字] |
| 05 | Content | 解决方案 | [含具体数字的结论句] | `CONTENT_MASTER` | `addHuaweiRichCard × 3` | — |
| 10 | Appendix | 附录 | 区域医院指标明细（42 行） | `APPENDIX_MASTER` | `addTable(... autoPage)` | — |
| N | Summary | 结论与行动 | [行动号召句] | `SUMMARY_MASTER` | `createSummarySlide` | — |

**大纲表格强制规则：**

- **标题列** — 必须是结论句/价值句，含具体数字优先。❌ "产品功能介绍" → ✅ "三大核心能力将交付周期压缩 40%"
- **Section 列** — 除封面/目录外，每张 slide 都要明确归属 section；Section Divider、内容页、总结页、附录页不得留空
- **Master 列** — 必须从 deck skeleton 的 master registry 中选择，不能写成“默认”或“到时再看”
- **核心组件列** — 具体到函数名。❌ "卡片布局" → ✅ `addHuaweiRichCard × 3`
- **⚠️ 待补充列** — 所有尚未获得的具体数字、比例、时间节点，全部列出
- **附录判定** — 超出风格安全密度的长表格，必须在大纲阶段就标为 `Appendix`，不能先塞进内容页再看是否溢出

### 3.3 数据缺口处理（确认前必须解决）

大纲中每个 `⚠️` 项，**必须通过以下一种方式解决后才能推进**：

**方式 A — 追问用户**（推荐，适合 1–3 个数据缺口）
优先使用结构化提问工具；若不可用，就在一条消息里一次性提问所有缺失数据点，并说明每个数字用在哪张幻灯片。

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

将**每张幻灯片**精确归类为以下 6 种页面类型之一：

| 类型 | 用途 |
|------|---------|
| Cover | 开场幻灯片 — 标题、副标题、日期/演讲者 |
| TOC | 目录 — 章节概览 |
| Section Divider | 主要章节之间的分隔页 |
| Content | 主要内容幻灯片 — 所有变体 |
| Appendix | 附录页 — 长表格、补充数据、明细清单 |
| Summary | 结尾 — 关键要点、行动号召、致谢 |

确保视觉多样性 — 不要在连续幻灯片中使用相同的内容布局。封面、目录、章节分隔、内容、总结的视觉细节请参阅当前 preset 文件的"5 种页面类型"章节；`Appendix` 属于 deck skeleton 层，默认沿用表格风格组件 + `APPENDIX_MASTER`。

## 第 4.1 步：先建立 deck skeleton（必须完成）

在写任何 slide 文件前，先在实现层定义整份 deck 的骨架：

- **master registry**：至少包含 `COVER_MASTER`、`TOC_MASTER`、`SECTION_MASTER`、`CONTENT_MASTER`、`SUMMARY_MASTER`
- **appendix registry**：存在长表格时，再增加 `APPENDIX_MASTER`
- **section map**：列出所有业务章节标题，确保与 TOC、章节分隔页、PPT section title 一致
- **slide manifest**：为每个 slide 指定 `file`、`type`、`masterName`、`sectionTitle`

推荐写成这样的内部清单：

```javascript
const slideManifest = [
  { file: "slide-01.js", type: "cover", masterName: "COVER_MASTER" },
  { file: "slide-02.js", type: "toc", masterName: "TOC_MASTER" },
  { file: "slide-03.js", type: "section", masterName: "SECTION_MASTER", sectionTitle: "市场机会" },
  { file: "slide-04.js", type: "content", masterName: "CONTENT_MASTER", sectionTitle: "市场机会" },
  { file: "slide-10.js", type: "appendix", masterName: "APPENDIX_MASTER", sectionTitle: "附录" },
];
```

## 第 4.2 步：定义 Master / Placeholder 合同

生成路径的高阶能力，核心不在“每页都手画一遍”，而在“master 画重复 chrome，slide 只填内容”。因此在进入第 5 步前先定义：

- 哪些固定元素进入 master：logo、页眉、页脚、页码轨道、标题底线、固定免责声明
- 哪些内容通过 placeholder 注入：`title`、`subtitle`、`body`、`chart`、`table`、`insight`、`media`
- 哪些内容仍用绝对坐标：非常规装饰、复杂图形、跨栏流程图、Rich Card 组合布局

规则：

- 相同语义槽位在不同风格中优先使用相同 placeholder 名，便于 compile.js 做统一编排
- 不要把完全动态的复杂布局硬塞进 placeholder；placeholder 适合标题、正文、图表区、表格区等稳定区域
- 明明可进入 master 的固定元素，不要在 slide 文件里重复绘制

## 第 4.3 步：建立 Section 合同

每个主要章节在编译前先注册为真实的 PPT section：

```javascript
pres.addSection({ title: "市场机会" });
pres.addSection({ title: "解决方案" });
pres.addSection({ title: "落地计划" });
pres.addSection({ title: "附录" });
```

随后在创建 slide 时显式指定 `sectionTitle`：

```javascript
const slide = pres.addSlide({
  masterName: "CONTENT_MASTER",
  sectionTitle: "解决方案",
});
```

约束：

- 封面和 TOC 可不属于任何 section
- Section Divider、Content、Appendix、Summary 均应属于某个 section
- TOC 展示名称、章节分隔页标题、`pres.addSection({ title })` 的标题三者必须完全一致

## 第 4.4 步：Appendix Table Auto-Paging 规划

当表格满足以下任一条件时，直接规划到 appendix，而不是硬塞内容页：

- 行数超过当前风格建议上限
- 列数超过 5 且无法通过删减保留结论
- 为塞进内容页必须把字号压到 10pt 以下
- 表格的主要价值是“备查明细”，不是“页面主结论”

Appendix 表格的实现约定：

- 使用 `APPENDIX_MASTER`
- 通过 placeholder 预留 `title`、`table`、`insight` 区
- `slide.addTable(..., { autoPage: true, autoPageRepeatHeader: true })`
- 多列表头时补上 `autoPageHeaderRows`
- 第一页说明“这是什么明细表”，后续自动分页页保持相同表头和 section 归属

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
- [ ] 每个主要章节已预注册为 PPT section
- [ ] master registry 已先于 slide 文件规划完成
- [ ] 需要长表格时：已规划 appendix slide，而非临时挤进内容页
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

安装依赖前先确认是否已可用；缺失时再安装：
```shell
npm install -g react-icons react react-dom sharp
```

使用图标时，**compile.js 整个文件必须包裹在 `(async () => { ... })()` 中**，因为 CommonJS 不支持顶层 `await`。完整写法见 mckinsey-style.md § 8 的 compile.js 示例。

## 第 5 步：生成幻灯片 JS 文件

在 `slides/` 中为每张幻灯片创建一个 JS 文件，每个文件导出一个同步的 `createSlide(pres, theme, ctx = {})` 函数。

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

如果运行环境支持并行 agent / subagent，可并行生成最多 5 张幻灯片；如果不支持，就顺序生成，但仍保持每张幻灯片的设计合同清晰独立。告知每个 agent：

1. 文件路径：`slides/slide-01.js`、`slides/slide-02.js` 等
2. 图片目录：`slides/imgs/`
3. 最终 PPTX：`slides/output/`
4. 尺寸：10" × 5.625"（LAYOUT_16x9）
5. 字体：中文 = `Microsoft YaHei`，英文 = `Arial`
6. 颜色：6 位十六进制，不带 `#`
7. theme 对象约定：仅 5 个键（`primary`、`secondary`、`accent`、`light`、`bg`）
8. master / section 约定：使用传入的 `ctx.masterName` 与 `ctx.sectionTitle`
9. **必须遵循精装交付标准**：每张内容页必须包含数据/统计、tagline、bullet 前缀、至少一种非文字视觉元素（SVG 图标/流程图/对比矩阵）、底部说明区
10. 必须遵循 [pptxgenjs.md](pptxgenjs.md)

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
//   母版      : CONTENT_MASTER
//   章节      : 市场机会
//   占位符    : title / subtitle / body
//   背景      : theme.bg（FFFFFF，与所有内容页一致）
//   页码标记   : slide 03

function createSlide(pres, theme, ctx = {}) {
  const slide = pres.addSlide({
    masterName: ctx.masterName || "CONTENT_MASTER",
    sectionTitle: ctx.sectionTitle || "市场机会",
  });

  slide.addText("AI triage cut follow-up delays by 37%", {
    placeholder: "title",
  });

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

创建 `slides/compile.js`。

> **如果演示文稿使用了 react-icons 图标**（步骤 4.8 中初始化了 `icon-utils.js`），整个 compile.js 文件必须包裹在 `(async () => { ... })()` 中，因为 `iconToBase64Png` 是异步函数。下方模板为不使用图标的同步版本；使用图标时参考步骤 4.8 的说明进行改写。

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

// ── 先注册 master，再注册 section ───────────────────────────────
pres.defineSlideMaster({ title: "COVER_MASTER", background: { color: theme.bg } });
pres.defineSlideMaster({ title: "TOC_MASTER", background: { color: theme.bg } });
pres.defineSlideMaster({ title: "SECTION_MASTER", background: { color: "EEF6FF" } });
pres.defineSlideMaster({ title: "CONTENT_MASTER", background: { color: theme.bg } });
pres.defineSlideMaster({ title: "SUMMARY_MASTER", background: { color: theme.bg } });
pres.defineSlideMaster({ title: "APPENDIX_MASTER", background: { color: "F8FAFC" } });

["市场机会", "解决方案", "落地计划", "附录"].forEach((title) => {
  pres.addSection({ title });
});

// ── 按 manifest 驱动，而不是裸遍历文件 ──────────────────────────
const slideManifest = [
  { file: "slide-01.js", masterName: "COVER_MASTER" },
  { file: "slide-02.js", masterName: "TOC_MASTER" },
  { file: "slide-03.js", masterName: "SECTION_MASTER", sectionTitle: "市场机会" },
  { file: "slide-04.js", masterName: "CONTENT_MASTER", sectionTitle: "市场机会" },
  { file: "slide-10.js", masterName: "APPENDIX_MASTER", sectionTitle: "附录" },
];

for (const spec of slideManifest) {
  const mod = require(path.join(__dirname, spec.file));
  mod.createSlide(pres, theme, spec);
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

PowerShell 等价写法：

```powershell
Set-Location slides
node .\compile.js
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
├── slide-10.js      # 附录长表格（可自动分页）
├── ...
├── compile.js       # 将所有幻灯片组合为 PPTX
├── imgs/            # 幻灯片引用的图片
└── output/
    └── presentation.pptx
```
