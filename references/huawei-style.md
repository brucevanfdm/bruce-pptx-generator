# Style Preset: 华为方案（Huawei Enterprise）

适合场景：产品介绍、公司介绍、解决方案汇报、技术架构展示、政企客户提案、招投标方案。追求模块清晰、结构工程感强、橙蓝双色权威视觉。

## 核心设计哲学

**华为方案 = 编号模块 × 橙蓝双色 × 工程结构感**

三大原则：
1. **模块编号驱动（Module-Numbered）** — 每张幻灯片的内容必须组织在清晰的编号框架内（① ② ③ 或 01 / 02 / 03），让受众第一眼看到结构，而非内容。
2. **解决方案导向（Solution-First）** — 每张内容页先抛出"能解决什么问题"或"能带来什么价值"，再展开技术/实现细节。痛点 → 方案 → 优势 → 验证。
3. **工程视觉语言（Engineering Visual）** — 优先使用架构层图、流程节点图、对比矩阵表达技术逻辑；橙色用于强调"关键节点/推荐选项/当前状态"，蓝色用于结构与层次。

## 默认叙事骨架

华为方案默认不是“罗列功能”，而是“像交付解决方案一样推进”：

1. 背景与痛点：行业问题、合规压力、建设缺口
2. 方案总览：一句主张 + 三层能力总图
3. 核心能力：能力模块、系统架构、关键机制
4. 实施路径：部署方式、交付节奏、集成边界
5. 验证与价值：案例、指标、ROI、风险收敛
6. 下一步：试点范围、资源需求、上线节奏

优先使用“架构总览页”和“部署拓扑页”建立工程可信度，而不是连续卡片墙。

## 签名页

这套风格应优先拥有以下 signature pages：

- **Architecture Overview**：分层架构 / 总线 / 平台能力栈，是整套风格最能拉开差异的页面
- **Deployment Topology**：总部-区域-边缘-终端的部署关系或接口边界
- **Capability Matrix**：能力模块 × 场景 / 客户对象 / 交付价值
- **Control Tower Summary**：关键指标、试点范围、价值证明的总览页

如果一份“华为方案”没有出现至少一张系统总览或部署页，通常说明它还停留在普通企业模板层。

## 禁用模式

- 禁止把橙色同时用于所有高亮、所有编号、所有标签、所有流程节点。橙色只保留给“关键节点 / 推荐项 / 当前状态 / 风险提示”。
- 禁止连续 3 张以上纯卡片页；至少穿插 1 张架构页、流程页或拓扑页。
- 禁止把产品能力页做成“营销文案集合”；华为方案需要模块边界、接口关系、交付含义。
- 禁止出现大面积无结构装饰色块。所有色块都要服务于模块、层次或流程。

## 图表与图形语法

- 图表优先回答“方案价值是否可验证”，而不是单纯展示数据存在。
- 优先使用 **architecture / process / comparison / roadmap / KPI dashboard**，再考虑饼图或自由图形。
- 条形图和折线图默认配右侧洞察区，必须解释“为什么这个结果重要”。
- 表格更偏“规格表 / 对比表 / 交付清单”，长明细优先移入 appendix，而不是压缩塞进内容页。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深海军蓝 | `0D2B4B` | 标题栏背景、主要文字、深色区块 |
| `secondary` | 天际蓝 | `0074CC` | 副标题、模块序号、强调蓝色 |
| `accent` | 华为橙 | `E87722` | 橙色模块标签、卡片顶线、当前节点 |
| `light` | 极浅蓝 | `EEF5FB` | 卡片背景、斑马行、浅色区 |
| `bg` | 纯白 | `FFFFFF` | 所有内容页背景 |
| `dividerBg` | 深海军蓝 | `0D2B4B` | 章节分隔页背景 |
| `bodyText` | 深炭 | `1A1A1A` | 正文段落 |
| `mutedText` | 中灰 | `5C5C5C` | 次级文字、说明、注释 |
| `headerText` | 纯白 | `FFFFFF` | 标题栏白色文字 |
| `border` | 浅蓝灰 | `C9DFF0` | 表格边框、卡片边框 |
| `orangeLight` | 浅橙 | `FFF0E5` | 橙色卡片浅色背景 |

```javascript
const theme = {
  primary:     "0D2B4B",
  secondary:   "0074CC",
  accent:      "E87722",
  light:       "EEF5FB",
  bg:          "FFFFFF",
  dividerBg:   "0D2B4B",
  bodyText:    "1A1A1A",
  mutedText:   "5C5C5C",
  headerText:  "FFFFFF",
  border:      "C9DFF0",
  orangeLight: "FFF0E5",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 30–36 | Bold | `headerText`（深蓝底） |
| 封面副标题 | Microsoft YaHei | 13–15 | Regular | `light` |
| 内容页标题 | Microsoft YaHei | 20–24 | Bold | `headerText`（深蓝标题栏） |
| 模块标签文字 | Arial | 12–14 | Bold | `headerText`（橙色底） |
| 二级标题 / 卡片标题 | Microsoft YaHei | 13–15 | Bold | `primary` |
| 三级标题 | Microsoft YaHei | 11–12 | Bold | `secondary` |
| 正文 | Microsoft YaHei | 10–12 | Regular | `bodyText` |
| 说明 / 来源 | Microsoft YaHei | 9–10 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 40–52 | Bold | `secondary` 或 `accent` |
| 表格表头 | Microsoft YaHei | 11 | Bold | `headerText`（`primary` 底） |
| 表格内容 | Microsoft YaHei | 10 | Regular | `bodyText` |
| 编号大字（章节页） | Arial Black | 100–120 | Bold | `FFFFFF`（透明度 80%） |

## 布局网格系统

幻灯片尺寸 10" × 5.625"。

**安全边界：**
- 左/右边距：`0.4"`
- 上边距（标题区以下）：`1.05"`
- 下边距：`0.35"`（页码区）
- 内容安全区：`x: 0.4–9.6`, `y: 1.05–5.25`

**华为式特有间距规范：**
- 标题区：深蓝标题栏（全宽 `h: 0.78`）+ 左侧橙色模块标签（`w: 0.7`）
- 模块编号卡片：左橙色竖线（`w: 0.05`）+ 橙色圆形编号（`r: 0.22`）
- 卡片间距：`≥ 0.15"`
- 三栏等分：每栏宽约 `2.87"`，间距 `0.15"`

**内容密度指引（方案汇报型 — 精装标准）：**

> 本风格定位为**方案汇报型**：每张幻灯片一个核心主张，配套 4–6 个模块化要点，每个要点必须有数据支撑、tagline 和底部说明。

- 每张内容页：要点 4–6 个（超出 6 个拆页，少于 4 个增加 tagline/数据/洞察补满空间）
- 每个要点：标题 ≤ 20 字 + tagline 1 句（12–20 字）+ 支撑说明 2–4 行
- 数据表格：最多 7 行 × 5 列
- 标题：必须是功能句或价值句，例："三层防护架构确保数据安全合规"
- **强制要求**：每张内容页至少包含 1 个非纯文字视觉元素（SVG 图标 / 流程图 / 进度环 / 对比矩阵 / KPI 卡）

## 标志性设计元素

### 1. 标题栏 + 模块标签（所有非封面页必用）

华为标志：深海军蓝全宽标题栏 + 左侧橙色模块标签 + 底部橙色细线。

```javascript
function addHuaweiSlideTitle(slide, pres, theme, title, moduleTag, source) {
  // 深蓝标题栏（全宽）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.78,
    fill: { color: theme.primary }
  });
  // 左侧橙色模块标签
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 0.68, h: 0.78,
    fill: { color: theme.accent }
  });
  // 模块标签文字
  if (moduleTag) {
    slide.addText(moduleTag, {
      x: 0, y: 0, w: 0.68, h: 0.78,
      fontSize: 12, fontFace: "Arial",
      color: theme.headerText, bold: true,
      align: "center", valign: "middle", margin: 0
    });
  }
  // 标题文字（白色）
  slide.addText(title, {
    x: 0.82, y: 0, w: 8.8, h: 0.78,
    fontSize: 22, fontFace: "Microsoft YaHei",
    color: theme.headerText, bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 橙色底部细线（标题栏下方）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0.78, w: 10, h: 0.04,
    fill: { color: theme.accent }
  });
  // 来源注释（可选，左下角小灰字）
  if (source) {
    slide.addText(`来源：${source}`, {
      x: 0.4, y: 5.05, w: 6, h: 0.2,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }
}
```

### 2. 页码徽章（所有非封面页必用）

```javascript
function addPageBadge(slide, pres, theme, num) {
  // 华为风：橙色胶囊，右下角
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 9.1, y: 5.15, w: 0.6, h: 0.35,
    fill: { color: theme.accent }
  });
  slide.addText(String(num), {
    x: 9.1, y: 5.15, w: 0.6, h: 0.35,
    fontSize: 11, fontFace: "Arial", color: theme.headerText,
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. 编号卡片（模块化要点卡）

华为标志性组件：左侧橙色竖条 + 橙色圆形序号 + 卡片内容。

```javascript
function addHuaweiNumberedCard(slide, pres, theme, x, y, w, h, num, title, desc, highlight) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h,
    fill: { color: highlight ? theme.orangeLight : theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 左侧橙色竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w: 0.06, h,
    fill: { color: highlight ? theme.accent : theme.secondary }
  });
  // 橙色圆形序号
  slide.addShape(pres.shapes.OVAL, {
    x: x + 0.16, y: y + 0.18, w: 0.44, h: 0.44,
    fill: { color: highlight ? theme.accent : theme.secondary }
  });
  slide.addText(String(num), {
    x: x + 0.16, y: y + 0.18, w: 0.44, h: 0.44,
    fontSize: 14, fontFace: "Arial Black",
    color: theme.headerText, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 卡片标题
  slide.addText(title, {
    x: x + 0.72, y: y + 0.1, w: w - 0.82, h: 0.4,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: highlight ? theme.accent : theme.primary,
    bold: true, align: "left", valign: "middle", margin: 0
  });
  // 分割线
  slide.addShape(pres.shapes.LINE, {
    x: x + 0.72, y: y + 0.52, w: w - 0.82, h: 0,
    line: { color: theme.border, width: 0.5 }
  });
  // 描述文字
  if (desc) {
    slide.addText(desc, {
      x: x + 0.72, y: y + 0.57, w: w - 0.82, h: h - 0.67,
      fontSize: 10, fontFace: "Microsoft YaHei",
      color: theme.bodyText, align: "left", valign: "top", margin: 0
    });
  }
}
```

### 3.5 精装能力卡片（Rich Card）—— 推荐默认使用

**优先使用此组件替代基础的 `addHuaweiNumberedCard`**。精装卡片包含：顶部强调线、编号圆形、标题、Tagline、带前缀的 bullet 功能列表、底部说明区。

```javascript
function addHuaweiRichCard(slide, pres, theme, x, y, w, h, num, title, tagline, features, detail, highlight) {
  const borderColor = highlight ? theme.accent : theme.secondary;
  const bgColor = highlight ? theme.orangeLight : theme.light;

  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h, fill: { color: bgColor }, line: { color: theme.border, width: 0.5 } });
  // 顶部强调线
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h: 0.07, fill: { color: borderColor } });

  // 编号圆形
  slide.addShape(pres.shapes.OVAL, { x: x + 0.18, y: y + 0.2, w: 0.5, h: 0.5, fill: { color: borderColor } });
  slide.addText(String(num), {
    x: x + 0.18, y: y + 0.2, w: 0.5, h: 0.5,
    fontSize: 16, fontFace: "Arial Black",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });

  // 标题
  slide.addText(title, {
    x: x + 0.78, y: y + 0.14, w: w - 0.95, h: 0.34,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: highlight ? theme.accent : theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });

  // Tagline
  slide.addText(tagline, {
    x: x + 0.78, y: y + 0.48, w: w - 0.95, h: 0.26,
    fontSize: 9.5, fontFace: "Microsoft YaHei",
    color: borderColor, bold: false,
    align: "left", valign: "middle", margin: 0
  });

  // 分隔线
  slide.addShape(pres.shapes.LINE, { x: x + 0.15, y: y + 0.82, w: w - 0.3, h: 0, line: { color: theme.border, width: 0.5 } });

  // Bullet 功能列表（带小方块前缀）
  const featStartY = y + 0.92;
  const featH = h < 2.0 ? 0.36 : 0.42;
  // 最多显示条数：保留底部说明区(0.58")后，计算可容纳行数，最多5条
  const footerReserve = detail ? 0.68 : 0.1;
  const maxFeats = Math.min(5, Math.floor((h - 0.92 - footerReserve) / featH));

  features.slice(0, maxFeats).forEach((f, i) => {
    const fy = featStartY + i * featH;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.18, y: fy + 0.12, w: 0.12, h: 0.12, fill: { color: borderColor } });
    slide.addText(f, {
      x: x + 0.38, y: fy + 0.05, w: w - 0.55, h: featH - 0.1,
      fontSize: 10, fontFace: "Microsoft YaHei", color: theme.bodyText,
      align: "left", valign: "middle", margin: 0
    });
  });

  // 底部说明区（如果有）
  if (detail) {
    const footerY = y + h - 0.58;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.15, y: footerY, w: w - 0.3, h: 0.48, fill: { color: "FFFFFF" }, line: { color: theme.border, width: 0.3 } });
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.15, y: footerY, w: 0.06, h: 0.48, fill: { color: theme.mutedText } });
    slide.addText(detail, {
      x: x + 0.28, y: footerY, w: w - 0.45, h: 0.48,
      fontSize: 8.5, fontFace: "Microsoft YaHei", color: theme.mutedText,
      align: "left", valign: "middle", margin: 0
    });
  }
}
```

### 3.6 痛点分析卡片（Pain Point Card）

适用于痛点/场景分析页。包含：顶部橙线、编号、标题、问题副标题、详细描述、数据影响标签，以及可选的 SVG 图标。

```javascript
function svgToBase64(svgStr) {
  // 统一使用 data: 前缀格式，与 addImage({ data: ... }) 兼容
  return "data:image/svg+xml;base64," + Buffer.from(svgStr).toString("base64");
}

function makePainPointCard(slide, pres, theme, x, y, w, h, num, title, subtitle, desc, impact, iconSvg) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h, fill: { color: theme.light }, line: { color: theme.border, width: 0.5 } });
  // 顶部橙线
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h: 0.06, fill: { color: theme.accent } });
  // 左侧竖条
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w: 0.06, h, fill: { color: theme.accent } });

  // 编号
  slide.addShape(pres.shapes.OVAL, { x: x + 0.18, y: y + 0.18, w: 0.48, h: 0.48, fill: { color: theme.accent } });
  slide.addText(String(num), { x: x + 0.18, y: y + 0.18, w: 0.48, h: 0.48, fontSize: 16, fontFace: "Arial Black", color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0 });

  // SVG 图标（右上角）
  if (iconSvg) {
    const iconData = svgToBase64(`<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg">${iconSvg}</svg>`);
    slide.addImage({ data: iconData, x: x + w - 0.95, y: y + 0.15, w: 0.75, h: 0.75 });
  }

  // 标题
  slide.addText(title, { x: x + 0.78, y: y + 0.12, w: w - 1.85, h: 0.32, fontSize: 14, fontFace: "Microsoft YaHei", color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0 });
  // 副标题
  slide.addText(subtitle, { x: x + 0.78, y: y + 0.44, w: w - 1.85, h: 0.28, fontSize: 10, fontFace: "Microsoft YaHei", color: theme.accent, bold: true, align: "left", valign: "middle", margin: 0 });
  // 分隔线
  slide.addShape(pres.shapes.LINE, { x: x + 0.15, y: y + 0.78, w: w - 0.3, h: 0, line: { color: theme.border, width: 0.5 } });
  // 描述
  slide.addText(desc, { x: x + 0.15, y: y + 0.84, w: w - 0.3, h: h - 1.12, fontSize: 9.5, fontFace: "Microsoft YaHei", color: theme.bodyText, align: "left", valign: "top", margin: 0, lineSpaceMult: 1.4 });
  // 影响标签
  slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.15, y: y + h - 0.38, w: 0.06, h: 0.28, fill: { color: theme.secondary } });
  slide.addText(impact, { x: x + 0.26, y: y + h - 0.38, w: w - 0.4, h: 0.28, fontSize: 9, fontFace: "Microsoft YaHei", color: theme.secondary, align: "left", valign: "middle", margin: 0 });
}
```

### 4. 数据表格（斑马行 + 深蓝表头）

```javascript
function addHuaweiTable(slide, pres, theme, x, y, w, h, headers, rows, highlightCol) {
  // highlightCol: 高亮列索引（推荐方案），传 undefined 则不高亮
  const colW = w / headers.length;
  const rowH = (h - 0.44) / rows.length;

  // 表头行
  headers.forEach((header, i) => {
    const isHL = i === highlightCol;
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + i * colW, y, w: colW, h: 0.44,
      fill: { color: isHL ? theme.accent : theme.primary }
    });
    slide.addText(header, {
      x: x + i * colW + 0.06, y, w: colW - 0.12, h: 0.44,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.headerText, bold: true,
      align: i === 0 ? "left" : "center", valign: "middle", margin: 0
    });
  });

  // 数据行（斑马行）
  rows.forEach((row, ri) => {
    const rowY = y + 0.44 + ri * rowH;
    const isEven = ri % 2 === 0;
    row.forEach((cell, ci) => {
      const isHL = ci === highlightCol;
      slide.addShape(pres.shapes.RECTANGLE, {
        x: x + ci * colW, y: rowY, w: colW, h: rowH,
        fill: { color: isHL ? theme.orangeLight : (isEven ? theme.light : theme.bg) },
        line: { color: theme.border, width: 0.3 }
      });
      slide.addText(cell, {
        x: x + ci * colW + 0.06, y: rowY, w: colW - 0.12, h: rowH,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: isHL ? theme.accent : theme.bodyText,
        bold: isHL,
        align: ci === 0 ? "left" : "center", valign: "middle", margin: 0
      });
    });
  });
}
```

### 5. KPI 数据卡（橙色顶线 + 大数值）

```javascript
function addHuaweiKpiCard(slide, pres, theme, x, y, w, h, value, unit, label, desc, useOrange) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h,
    fill: { color: useOrange ? theme.orangeLight : theme.light },
    line: { color: useOrange ? theme.accent : theme.border, width: 0.5 }
  });
  // 顶部强调线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.06,
    fill: { color: useOrange ? theme.accent : theme.secondary }
  });
  // 大数值
  slide.addText(value, {
    x: x + 0.1, y: y + 0.15, w: w - 0.2, h: 0.75,
    fontSize: 44, fontFace: "Arial Black",
    color: useOrange ? theme.accent : theme.secondary,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // 单位（右上角小字）
  if (unit) {
    slide.addText(unit, {
      x: x + w * 0.55, y: y + 0.18, w: w * 0.42, h: 0.28,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: useOrange ? theme.accent : theme.secondary,
      bold: true, align: "left", valign: "top", margin: 0
    });
  }
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + 0.95, w: w - 0.2, h: 0.34,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "center", margin: 0
  });
  // 说明
  if (desc) {
    slide.addText(desc, {
      x: x + 0.1, y: y + 1.32, w: w - 0.2, h: 0.32,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "center", margin: 0
    });
  }
}
```

### 6. 要点列表（橙色方块前缀）

```javascript
function addHuaweiBulletSection(slide, pres, theme, x, y, w, items) {
  // items: [{ text, level, bold, highlight }]  level: 0=主要, 1=次级
  let curY = y;
  items.forEach(item => {
    const isMain = item.level === 0;
    const indent = isMain ? 0 : 0.28;
    const fs = isMain ? 12 : 10;
    const dotColor = item.highlight ? theme.accent : (isMain ? theme.secondary : theme.border);
    const lineH = isMain ? 0.34 : 0.28;
    const gap = isMain ? 0.1 : 0.07;

    // 前缀方块（主要：实心橙/蓝；次级：空心边框灰）
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + indent, y: curY + (lineH - 0.1) / 2, w: 0.1, h: 0.1,
      fill: { color: dotColor }
    });
    slide.addText(item.text, {
      x: x + indent + 0.18, y: curY, w: w - indent - 0.18, h: lineH,
      fontSize: fs, fontFace: "Microsoft YaHei",
      color: item.highlight ? theme.accent : (isMain ? theme.bodyText : theme.mutedText),
      bold: item.bold || false,
      align: "left", valign: "middle", margin: 0
    });
    curY += lineH + gap;
  });
  return curY; // 返回当前 Y 位置，方便连续排列
}
```

### 7. 章节分隔页

```javascript
function createHuaweiSectionDivider(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 左侧橙色竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.6, y: 1.0, w: 0.1, h: 3.4,
    fill: { color: theme.accent }
  });
  // 章节编号（大字，半透明白）
  slide.addText(String(num).padStart(2, '0'), {
    x: 0.85, y: 0.5, w: 3.5, h: 2.2,
    fontSize: 110, fontFace: "Arial Black",
    color: "FFFFFF", bold: true,
    align: "left", margin: 0,
    transparency: 82
  });
  // 橙色分割短线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.85, y: 2.6, w: 1.2, h: 0.06,
    fill: { color: theme.accent }
  });
  // 章节标题（白色）
  slide.addText(title, {
    x: 0.85, y: 2.75, w: 8.4, h: 0.9,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 副标题
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.85, y: 3.72, w: 8.4, h: 0.36,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.light, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 8. 图表（数据可视化）

**图表必须配合 Action Title 表达数据结论，不作纯装饰。**

```javascript
function addHuaweiChart(slide, pres, theme, type, chartData, opts = {}) {
  const defaults = {
    chartColors: [theme.secondary, theme.accent, "3399FF", "FF9944", "006BB3"],
    chartArea: { fill: { color: theme.bg } },
    catAxisLabelColor: theme.mutedText,
    valAxisLabelColor: theme.mutedText,
    valGridLine: { color: theme.border, size: 0.5 },
    catGridLine: { style: "none" },
    showValue: true,
    dataLabelColor: theme.bodyText,
    dataLabelFontSize: 10,
    dataLabelFontFace: "Arial",
    showLegend: chartData.length > 1,
    legendPos: "b",
    legendFontSize: 10,
    legendFontFace: "Microsoft YaHei",
    legendColor: theme.mutedText,
  };
  slide.addChart(type, chartData, { ...defaults, ...opts });
}
```

**图表 + 右侧洞察布局（左 60% 图表 + 右 40% 要点）：**

```javascript
function createChartWithInsightsSlide(pres, theme, title, moduleTag, chartData, chartType, insights, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addHuaweiSlideTitle(slide, pres, theme, title, moduleTag, source);

  // 左侧图表区
  addHuaweiChart(slide, pres, theme, chartType, chartData, {
    x: 0.4, y: 1.0, w: 5.7, h: 3.95,
    barDir: "col",
    dataLabelPosition: "outEnd",
  });

  // 右侧分隔线
  slide.addShape(pres.shapes.LINE, {
    x: 6.3, y: 1.1, w: 0, h: 3.75,
    line: { color: theme.border, width: 0.75 }
  });

  // 右侧洞察要点（最多 3 条）
  insights.slice(0, 3).forEach((item, i) => {
    const iy = 1.15 + i * 1.3;
    // 橙色编号方块
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 6.5, y: iy, w: 0.34, h: 0.34,
      fill: { color: i === 0 ? theme.accent : theme.secondary }
    });
    slide.addText(String(i + 1), {
      x: 6.5, y: iy, w: 0.34, h: 0.34,
      fontSize: 12, fontFace: "Arial", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    slide.addText(item.title, {
      x: 6.95, y: iy, w: 2.65, h: 0.34,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    if (item.desc) {
      slide.addText(item.desc, {
        x: 6.95, y: iy + 0.38, w: 2.65, h: 0.75,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.mutedText, align: "left", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 9. SVG 内联图形（零依赖，完全同步）

无需任何外部库。在 Node.js 生成 SVG 字符串，转 base64 嵌入幻灯片。

```javascript
function svgToBase64(svgStr) {
  // 统一使用 data: 前缀格式，与 addImage({ data: ... }) 兼容
  return "data:image/svg+xml;base64," + Buffer.from(svgStr).toString("base64");
}
```

**三层技术架构图（产品 / 方案架构必备）：**

```javascript
function makeHuaweiArchitecture(layers, w = 800, h = 320) {
  // layers: [{ label, sublabel, color? }]，从上到下（顶层 = 应用层）
  // 建议 3 层：应用层、平台层、基础设施层
  const n = layers.length;
  const padH = 20, layerH = (h - padH * 2) / n, gap = 6;
  const colors = ["0D2B4B", "0074CC", "3399FF"];

  const rects = layers.map((layer, i) => {
    const y = padH + i * (layerH + gap);
    const indentLeft = i * 20;
    const lw = w - indentLeft * 2;
    const bg = layer.color || colors[i % colors.length];
    const fs = Math.min(16, Math.round(layerH * 0.28));
    const subfs = Math.round(fs * 0.75);
    return `
      <rect x="${indentLeft}" y="${y}" width="${lw}" height="${layerH}" rx="4" fill="#${bg}"/>
      <text x="${w / 2}" y="${y + layerH / 2 - (layer.sublabel ? fs * 0.5 : 0)}" text-anchor="middle"
        font-size="${fs}" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${layer.label}</text>
      ${layer.sublabel ? `<text x="${w / 2}" y="${y + layerH / 2 + fs * 0.9}" text-anchor="middle"
        font-size="${subfs}" font-family="Microsoft YaHei,Arial" fill="rgba(255,255,255,0.82)">${layer.sublabel}</text>` : ""}
    `;
  });

  // 右侧橙色竖线装饰
  const sideBar = `<rect x="${w - 8}" y="${padH}" width="6" height="${h - padH * 2}" rx="3" fill="#E87722"/>`;

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${sideBar}${rects.join("")}
  </svg>`);
}
// 用法（3 层方案架构）
const arch = makeHuaweiArchitecture([
  { label: "应用层",         sublabel: "Portal / APP / API 开放平台" },
  { label: "平台能力层",     sublabel: "数据中台 / AI 引擎 / 安全管控" },
  { label: "基础设施层",     sublabel: "云计算 / 网络 / 存储 / 硬件" },
]);
slide.addImage({ data: arch, x: 0.5, y: 1.1, w: 9.0, h: 3.5 });
```

**横向流程节点图（实施步骤 / 业务流程）：**

```javascript
function makeHuaweiProcess(steps, w = 860, h = 160) {
  // steps: [{ num, label, desc?, active? }]  active = 橙色高亮
  const n = steps.length;
  const padH = 20, nodeR = 30, lineY = h / 2;
  const step = (w - padH * 2) / Math.max(n - 1, 1);

  const lines = steps.slice(0, -1).map((_, i) => {
    const x1 = padH + i * step + nodeR;
    const x2 = padH + (i + 1) * step - nodeR;
    return `<line x1="${x1}" y1="${lineY}" x2="${x2}" y2="${lineY}"
      stroke="#C9DFF0" stroke-width="2.5"/>
      <polygon points="${x2},${lineY - 5} ${x2 + 10},${lineY} ${x2},${lineY + 5}" fill="#C9DFF0"/>`;
  }).join("");

  const nodes = steps.map((s, i) => {
    const cx = padH + i * step;
    const fill = s.active ? "E87722" : "0074CC";
    const ring = s.active ? `<circle cx="${cx}" cy="${lineY}" r="${nodeR + 6}"
      fill="none" stroke="#E87722" stroke-width="2" opacity="0.4"/>` : "";
    return `
      ${ring}
      <circle cx="${cx}" cy="${lineY}" r="${nodeR}" fill="#${fill}"/>
      <text x="${cx}" y="${lineY - 6}" text-anchor="middle"
        font-size="11" font-weight="bold" font-family="Arial" fill="white">${s.num || String(i + 1).padStart(2, '0')}</text>
      <text x="${cx}" y="${lineY + 11}" text-anchor="middle"
        font-size="12" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${s.label}</text>
      ${s.desc ? `<text x="${cx}" y="${lineY + nodeR + 18}" text-anchor="middle"
        font-size="10" font-family="Microsoft YaHei,Arial" fill="#5C5C5C">${s.desc}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${lines}${nodes.join("")}
  </svg>`);
}
// 用法（4 步实施路径）
const process = makeHuaweiProcess([
  { label: "需求调研",  desc: "现状分析" },
  { label: "方案设计",  desc: "架构规划" },
  { label: "部署实施",  desc: "上线交付", active: true },
  { label: "运营优化",  desc: "持续迭代" },
]);
slide.addImage({ data: process, x: 0.5, y: 2.6, w: 9.0, h: 1.9 });
```

**进度环（目标达成 / 覆盖率 / 完成率）：**

```javascript
function makeProgressRing(percent, fgColor, bgColor, label, size = 200) {
  const r = 74, cx = size / 2, cy = size / 2;
  const circ = 2 * Math.PI * r;
  const dash = (circ * percent / 100).toFixed(1);
  return svgToBase64(`
    <svg width="${size}" height="${size}" xmlns="http://www.w3.org/2000/svg">
      <circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="#${bgColor}" stroke-width="14"/>
      <circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="#${fgColor}" stroke-width="14"
        stroke-dasharray="${dash} ${circ.toFixed(1)}" stroke-linecap="round"
        transform="rotate(-90 ${cx} ${cy})"/>
      <text x="${cx}" y="${cy - 6}" text-anchor="middle"
        font-size="40" font-weight="bold" font-family="Arial" fill="#${fgColor}">${percent}%</text>
      <text x="${cx}" y="${cy + 22}" text-anchor="middle"
        font-size="14" font-family="Arial" fill="#5C5C5C">${label || ""}</text>
    </svg>
  `);
}
// 用法
const ring = makeProgressRing(78, "E87722", "FFF0E5", "目标达成");
slide.addImage({ data: ring, x: 1.0, y: 1.3, w: 1.5, h: 1.5 });
```

**横向对比条（方案优势对比 / 维度评分）：**

```javascript
function makeHuaweiHBar(items, barColor, bgColor, chartW = 400) {
  const barH = 22, gap = 12, labelW = 100, maxBarW = chartW - labelW - 55;
  const maxVal = Math.max(...items.map(d => d.value));
  const rows = items.map((d, i) => {
    const y = i * (barH + gap) + 16;
    const bw = Math.round((d.value / maxVal) * maxBarW);
    const isHighlight = d.highlight;
    const color = isHighlight ? "E87722" : barColor;
    return `
      <text x="0" y="${y + barH * 0.72}" font-size="13" font-family="Microsoft YaHei,Arial" fill="#5C5C5C">${d.label}</text>
      <rect x="${labelW}" y="${y}" width="${maxBarW}" height="${barH}" rx="3" fill="#${bgColor}"/>
      <rect x="${labelW}" y="${y}" width="${bw}" height="${barH}" rx="3" fill="#${color}"/>
      <text x="${labelW + bw + 8}" y="${y + barH * 0.72}" font-size="13" font-family="Arial Black" fill="#${color}">${d.value}${d.unit || ""}</text>
    `;
  }).join("");
  const svgH = items.length * (barH + gap) + 20;
  return svgToBase64(`<svg width="${chartW}" height="${svgH}" xmlns="http://www.w3.org/2000/svg">${rows}</svg>`);
}
// 用法
const hbar = makeHuaweiHBar([
  { label: "响应速度",   value: 96, unit: "分",  highlight: true },
  { label: "安全防护",   value: 88, unit: "分" },
  { label: "扩展能力",   value: 82, unit: "分" },
  { label: "运维成本",   value: 75, unit: "分" },
], "0074CC", "EEF5FB");
slide.addImage({ data: hbar, x: 0.5, y: 1.2, w: 5.5, h: 2.0 });
```

**里程碑路线图（带橙色当前节点）：**

```javascript
function makeHuaweiRoadmap(milestones, w = 860, h = 160) {
  const n = milestones.length;
  const padH = 50, lineY = h * 0.48;
  const stepW = (w - padH * 2) / Math.max(n - 1, 1);
  const currIdx = milestones.findIndex(m => m.current);

  const bgLine = `<line x1="${padH}" y1="${lineY}" x2="${w - padH}" y2="${lineY}"
    stroke="#C9DFF0" stroke-width="2.5"/>`;
  const doneX = currIdx >= 0 ? (padH + currIdx * stepW).toFixed(1) : padH;
  const progressLine = currIdx > 0
    ? `<line x1="${padH}" y1="${lineY}" x2="${doneX}" y2="${lineY}"
        stroke="#0074CC" stroke-width="2.5"/>` : "";

  const nodes = milestones.map((m, i) => {
    const cx = padH + i * stepW;
    const isDone = m.done || (currIdx >= 0 && i < currIdx);
    const isCurrent = m.current;
    const r = isCurrent ? 11 : 7;
    const fill = isDone ? "0074CC" : (isCurrent ? "E87722" : "FFFFFF");
    const stroke = isDone ? "0074CC" : (isCurrent ? "E87722" : "C9DFF0");
    const ring = isCurrent
      ? `<circle cx="${cx.toFixed(1)}" cy="${lineY}" r="18"
           fill="none" stroke="#E87722" stroke-width="2" opacity="0.4"/>` : "";
    return `
      ${ring}
      <circle cx="${cx.toFixed(1)}" cy="${lineY}" r="${r}" fill="#${fill}" stroke="#${stroke}" stroke-width="2.5"/>
      <text x="${cx.toFixed(1)}" y="${(lineY - r - 8).toFixed(1)}" text-anchor="middle"
        font-size="10" font-family="Arial" fill="#5C5C5C">${m.date || ""}</text>
      <text x="${cx.toFixed(1)}" y="${(lineY + r + 16).toFixed(1)}" text-anchor="middle"
        font-size="${isCurrent ? 13 : 11}" font-weight="${isCurrent ? "bold" : "normal"}"
        font-family="Microsoft YaHei,Arial"
        fill="#${isCurrent ? "E87722" : (isDone ? "1A1A1A" : "5C5C5C")}">${m.title}</text>
      ${m.desc ? `<text x="${cx.toFixed(1)}" y="${(lineY + r + 30).toFixed(1)}" text-anchor="middle"
        font-size="9" font-family="Microsoft YaHei,Arial" fill="#5C5C5C">${m.desc}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${bgLine}${progressLine}${nodes.join("")}
  </svg>`);
}
// 用法
const roadmap = makeHuaweiRoadmap([
  { date: "2024 Q1", title: "立项启动",  done: true },
  { date: "2024 Q2", title: "方案交付",  done: true },
  { date: "2024 Q3", title: "试点上线",  current: true, desc: "进行中" },
  { date: "2024 Q4", title: "全量部署" },
  { date: "2025 Q1", title: "效益评估" },
]);
slide.addImage({ data: roadmap, x: 0.4, y: 2.9, w: 9.2, h: 1.7 });
```

**金字塔图（价值模型 / 能力层级）：**

```javascript
function makePyramid(layers, colors, w = 500, h = 360) {
  const n = layers.length;
  const topW = w * 0.12, botW = w * 0.90;
  const cx = w / 2, layerH = h / n;

  const shapes = layers.map((layer, i) => {
    const wTop = topW + (botW - topW) * (i / n);
    const wBot = topW + (botW - topW) * ((i + 1) / n);
    const y = i * layerH;
    const pts = [
      `${(cx - wTop / 2).toFixed(1)},${y}`,
      `${(cx + wTop / 2).toFixed(1)},${y}`,
      `${(cx + wBot / 2).toFixed(1)},${(y + layerH).toFixed(1)}`,
      `${(cx - wBot / 2).toFixed(1)},${(y + layerH).toFixed(1)}`,
    ].join(" ");
    const color = colors[i % colors.length];
    const textY = y + layerH / 2;
    const fs = Math.min(16, Math.round(layerH * 0.32));
    return `
      <polygon points="${pts}" fill="#${color}" stroke="white" stroke-width="2"/>
      <text x="${cx}" y="${textY + fs * 0.35}" text-anchor="middle"
        font-size="${fs}" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${layer.label}</text>
      ${layer.value ? `<text x="${cx}" y="${textY + fs * 1.2}" text-anchor="middle"
        font-size="${Math.round(fs * 0.75)}" font-family="Arial" fill="rgba(255,255,255,0.85)">${layer.value}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">${shapes.join("")}</svg>`);
}
// 用法（华为方案价值模型）
const pyramid = makePyramid([
  { label: "业务价值",  value: "降本增效 · 竞争力提升" },
  { label: "数据能力",  value: "实时洞察 · 智能决策" },
  { label: "平台支撑",  value: "云原生 · 弹性扩展" },
  { label: "基础设施",  value: "安全合规 · 稳定可靠" },
], ["0D2B4B", "0074CC", "3399FF", "66B2FF"]);
slide.addImage({ data: pyramid, x: 0.5, y: 1.1, w: 4.8, h: 3.5 });
```

**方案特性对比矩阵（含推荐列高亮）：**

```javascript
function addHuaweiComparisonGrid(slide, pres, theme, x, y, w, h, options, features, cells, recommendIdx) {
  // recommendIdx: 推荐方案列索引（橙色高亮）
  const nOpts = options.length;
  const nFeat = features.length;
  const labelColW = w * 0.30;
  const optColW = (w - labelColW) / nOpts;
  const headerH = 0.40;
  const rowH = (h - headerH) / nFeat;

  // 表头角落
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w: labelColW, h: headerH,
    fill: { color: theme.primary }
  });

  options.forEach((opt, i) => {
    const cx = x + labelColW + i * optColW;
    const isRecommend = i === recommendIdx;
    slide.addShape(pres.shapes.RECTANGLE, {
      x: cx, y, w: optColW, h: headerH,
      fill: { color: isRecommend ? theme.accent : theme.secondary }
    });
    if (isRecommend) {
      // 推荐标签：叠加在表头左上角（白色文字，不超出表头边界）
      slide.addText("★ 推荐", {
        x: cx, y: y, w: optColW * 0.55, h: headerH * 0.42,
        fontSize: 8, fontFace: "Microsoft YaHei",
        color: "FFFFFF", bold: true, align: "left",
        margin: [0, 0, 0, 4]
      });
    }
    slide.addText(opt, {
      x: cx + 0.05, y: isRecommend ? y + headerH * 0.35 : y,
      w: optColW - 0.1, h: isRecommend ? headerH * 0.65 : headerH,
      fontSize: 11, fontFace: "Microsoft YaHei", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
  });

  features.forEach((feat, ri) => {
    const ry = y + headerH + ri * rowH;
    const rowBg = ri % 2 === 0 ? theme.light : theme.bg;

    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: ry, w: labelColW, h: rowH,
      fill: { color: rowBg }
    });
    slide.addText(feat, {
      x: x + 0.1, y: ry, w: labelColW - 0.15, h: rowH,
      fontSize: 10, fontFace: "Microsoft YaHei", color: theme.primary,
      bold: true, align: "left", valign: "middle", margin: 0
    });

    options.forEach((_, ci) => {
      const cx = x + labelColW + ci * optColW;
      const isRecommend = ci === recommendIdx;
      const val = (cells[ri] || [])[ci] || "";
      slide.addShape(pres.shapes.RECTANGLE, {
        x: cx, y: ry, w: optColW, h: rowH,
        fill: { color: isRecommend ? theme.orangeLight : rowBg },
        line: { color: theme.border, width: 0.3 }
      });
      let display = val, color = theme.bodyText, fs = 10, bold = false;
      if (val === "yes")     { display = "✓"; color = "107C41"; fs = 14; bold = true; }
      else if (val === "no") { display = "✗"; color = "C0392B"; fs = 14; bold = true; }
      else if (val === "partial") { display = "◐"; color = theme.secondary; fs = 14; bold = true; }
      else if (isRecommend)  { color = theme.accent; bold = true; }
      slide.addText(display, {
        x: cx, y: ry, w: optColW, h: rowH,
        fontSize: fs, fontFace: fs > 10 ? "Arial" : "Microsoft YaHei",
        color, bold, align: "center", valign: "middle", margin: 0
      });
    });
  });

  // 标签列右侧分隔线
  slide.addShape(pres.shapes.LINE, {
    x: x + labelColW, y, w: 0, h,
    line: { color: theme.border, width: 0.5 }
  });
}
// 用法
addHuaweiComparisonGrid(slide, pres, theme, 0.4, 1.05, 9.2, 4.1,
  ["华为方案", "方案B", "现有系统"],
  ["部署方式", "安全等级", "弹性扩容", "运维成本", "交付周期", "本地化支持"],
  [
    ["云 + 边缘",  "混合云",   "本地部署"],
    ["yes",        "partial",  "no"      ],
    ["yes",        "yes",      "no"      ],
    ["低",         "中",       "高"      ],
    ["4 个月",     "6 个月",   "10 个月" ],
    ["yes",        "partial",  "yes"     ],
  ],
  0  // 推荐列索引
);
```

**SWOT 四象限分析页：**

```javascript
function createHuaweiSWOTSlide(pres, theme, title, moduleTag, swot, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addHuaweiSlideTitle(slide, pres, theme, title, moduleTag, source);

  const defs = [
    { key: "S", label: "优势 Strengths",     color: theme.primary,   items: swot.S, col: 0, row: 0 },
    { key: "W", label: "劣势 Weaknesses",    color: theme.secondary, items: swot.W, col: 1, row: 0 },
    { key: "O", label: "机会 Opportunities", color: theme.accent,    items: swot.O, col: 0, row: 1 },
    { key: "T", label: "威胁 Threats",       color: "595959",        items: swot.T, col: 1, row: 1 },
  ];

  const qw = 4.5, qh = 1.92, startX = 0.4, startY = 1.0, gap = 0.1;
  const headerH = 0.36, itemH = 0.28;

  defs.forEach(q => {
    const x = startX + q.col * (qw + gap);
    const y = startY + q.row * (qh + gap);

    slide.addShape(pres.shapes.RECTANGLE, { x, y, w: qw, h: headerH, fill: { color: q.color } });
    slide.addText(q.key, {
      x, y, w: 0.36, h: headerH,
      fontSize: 14, fontFace: "Arial Black", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    slide.addText(q.label, {
      x: x + 0.4, y, w: qw - 0.4, h: headerH,
      fontSize: 11, fontFace: "Microsoft YaHei", color: theme.headerText,
      bold: true, align: "left", valign: "middle", margin: 0
    });
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: y + headerH, w: qw, h: qh - headerH,
      fill: { color: theme.light },
      line: { color: theme.border, width: 0.5 }
    });

    let curY = y + headerH + 0.08;
    (q.items || []).slice(0, 4).forEach(item => {
      slide.addShape(pres.shapes.RECTANGLE, {
        x: x + 0.12, y: curY + 0.09, w: 0.08, h: 0.08,
        fill: { color: q.color }
      });
      slide.addText(item, {
        x: x + 0.26, y: curY, w: qw - 0.36, h: itemH,
        fontSize: 10, fontFace: "Microsoft YaHei", color: theme.bodyText,
        align: "left", valign: "middle", margin: 0
      });
      curY += itemH;
    });
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**雷达图（能力评估 / 方案竞争力）：**

```javascript
function addHuaweiRadarChart(slide, pres, theme, x, y, w, h, dimensions, seriesData) {
  slide.addChart(pres.charts.RADAR, seriesData.map(s => ({
    name: s.name, labels: dimensions, values: s.values
  })), {
    x, y, w, h,
    radarStyle: "marker",
    chartColors: [theme.secondary, theme.accent, "3399FF"],
    chartArea: { fill: { color: theme.bg } },
    catAxisLabelColor: theme.mutedText,
    valGridLine: { color: theme.border, size: 0.5 },
    showLegend: seriesData.length > 1,
    legendPos: "b",
    legendFontSize: 10,
    legendFontFace: "Microsoft YaHei",
    legendColor: theme.mutedText,
  });
}
// 用法
addHuaweiRadarChart(slide, pres, theme, 0.4, 1.1, 5.5, 4.0,
  ["安全性", "稳定性", "扩展性", "易用性", "成本效益", "本地支持"],
  [
    { name: "华为方案", values: [92, 90, 88, 82, 78, 95] },
    { name: "竞品方案", values: [75, 80, 72, 76, 85, 60] },
  ]
);
```

## 视觉选择决策树

根据内容类型选择合适的视觉组件，避免全文字布局。**优先使用精装组件，基础组件仅作为降级方案。**

| 内容类型 | 推荐组件（精装优先） |
|---------|---------|
| 产品能力/功能模块 | **`addHuaweiRichCard`**（tagline + bullet + 底部说明） |
| 痛点/场景分析 | **`makePainPointCard`**（图标 + 数据标签 + 副标题） |
| 时间序列趋势 | `addHuaweiChart(LINE)` |
| 类别对比（5 项以内） | `addHuaweiChart(BAR)` |
| 数据 + 洞察 | `createChartWithInsightsSlide` |
| 构成比例 | `addHuaweiChart(PIE/DOUGHNUT)` |
| 多维横向对比 | `makeHuaweiHBar` (SVG) |
| KPI 大数字 | `addHuaweiKpiCard` |
| 完成率 / 目标达成 | `makeProgressRing` (SVG) |
| 流程步骤 / 实施路径 | `makeHuaweiProcess` (SVG) |
| 里程碑 / 路线图 | `makeHuaweiRoadmap` (SVG) |
| 系统分层架构 | `makeHuaweiArchitecture` (SVG) |
| 价值模型 / 能力层级 | `makePyramid` (SVG) |
| 方案选型对比 | `addHuaweiComparisonGrid` |
| 多维能力评分 | `addHuaweiRadarChart` |
| 战略分析框架 | `createHuaweiSWOTSlide` |
| 模块化要点（降级） | `addHuaweiNumberedCard` |
| 层级要点 | `addHuaweiBulletSection` |

**强制规则：**
- **每张 Content 页至少包含一种非纯文字的视觉组件**（SVG 图标、流程图、进度环、架构图、数据卡、KPI 卡）
- **封面页必须有装饰性视觉元素**（几何图形、能力矩阵、数据流线等），禁止只有标题+日期
- **基础 `addHuaweiNumberedCard(title, desc)` 视为毛坯房组件**，仅在空间极度受限时使用

## 5 种页面类型

### Cover（封面）

深蓝左侧色带（含橙色装饰斜切）+ 白色右侧区域 + 产品/方案视觉。

```javascript
function createHuaweiCoverSlide(pres, theme, title, subtitle, tag, dateStr) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧深蓝色带（约 40% 宽度）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 4.2, h: 5.625,
    fill: { color: theme.primary }
  });
  // 橙色细竖线（色带右边界）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 4.2, y: 0, w: 0.07, h: 5.625,
    fill: { color: theme.accent }
  });
  // 左下角橙色装饰块
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 4.6, w: 4.2, h: 1.025,
    fill: { color: theme.secondary }
  });
  // 橙色小横线（标题上方）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.4, y: 1.15, w: 0.8, h: 0.07,
    fill: { color: theme.accent }
  });
  // 产品/方案标签
  if (tag) {
    slide.addText(tag, {
      x: 0.4, y: 1.3, w: 3.4, h: 0.32,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.light, align: "left", margin: 0
    });
  }
  // 主标题（白色，左侧色带内）
  slide.addText(title, {
    x: 0.4, y: 1.7, w: 3.5, h: 2.0,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "top", margin: 0
  });
  // 副标题
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.4, y: 3.85, w: 3.5, h: 0.55,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.light, align: "left", margin: 0
    });
  }
  // 日期
  if (dateStr) {
    slide.addText(dateStr, {
      x: 0.4, y: 4.7, w: 3.5, h: 0.35,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.headerText, align: "left", margin: 0
    });
  }

  // 右侧核心价值标语（可选）
  slide.addText("打造数字化转型核心引擎", {
    x: 4.55, y: 2.2, w: 5.1, h: 0.55,
    fontSize: 17, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", margin: 0
  });

  return slide;
}
```

### Cover 精装版（推荐默认使用）

**`createRichCover` — 替代基础 `createHuaweiCoverSlide`。** 增加右侧能力矩阵卡片（3 个关键指标或能力标签），以及底部价值条，让封面不再是纯文字。

```javascript
/**
 * @param {string} title       - 演示主标题
 * @param {string} subtitle    - 副标题/定位语（1 行）
 * @param {string} tag         - 方案/产品标签（如"智慧医疗解决方案"）
 * @param {string} dateStr     - 日期或公司名
 * @param {Array}  metrics     - 右侧 3 个关键指标，每项 { value, unit, label }
 *                               例：[{ value: "95%", unit: "", label: "识别准确率" }, ...]
 * @param {string} valueSlogan - 右侧价值主张大字（1–2 行）
 */
function createRichCover(pres, theme, title, subtitle, tag, dateStr, metrics, valueSlogan) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧深蓝主色带
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 0, w: 4.4, h: 5.625, fill: { color: theme.primary } });
  // 橙色边界细线
  slide.addShape(pres.shapes.RECTANGLE, { x: 4.4, y: 0, w: 0.06, h: 5.625, fill: { color: theme.accent } });
  // 左下角次色填充块
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 4.5, w: 4.4, h: 1.125, fill: { color: theme.secondary } });
  // 橙色装饰横线（标题上方）
  slide.addShape(pres.shapes.RECTANGLE, { x: 0.4, y: 1.1, w: 1.0, h: 0.06, fill: { color: theme.accent } });

  // 方案标签
  if (tag) {
    slide.addText(tag, { x: 0.4, y: 1.24, w: 3.6, h: 0.3, fontSize: 11, fontFace: "Microsoft YaHei", color: theme.light, align: "left", margin: 0 });
  }
  // 主标题
  slide.addText(title, { x: 0.4, y: 1.62, w: 3.6, h: 2.0, fontSize: 26, fontFace: "Microsoft YaHei", color: "FFFFFF", bold: true, align: "left", valign: "top", margin: 0, lineSpaceMult: 1.3 });
  // 副标题
  if (subtitle) {
    slide.addText(subtitle, { x: 0.4, y: 3.72, w: 3.6, h: 0.5, fontSize: 11, fontFace: "Microsoft YaHei", color: theme.light, align: "left", margin: 0 });
  }
  // 日期/公司
  if (dateStr) {
    slide.addText(dateStr, { x: 0.4, y: 4.62, w: 3.6, h: 0.32, fontSize: 10, fontFace: "Microsoft YaHei", color: theme.headerText, align: "left", margin: 0 });
  }

  // ── 右侧区域 ──────────────────────────────────────────────
  // 价值主张大字
  if (valueSlogan) {
    slide.addText(valueSlogan, { x: 4.7, y: 0.6, w: 5.0, h: 0.9, fontSize: 18, fontFace: "Microsoft YaHei", color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0, lineSpaceMult: 1.3 });
    // 蓝色强调下划线
    slide.addShape(pres.shapes.RECTANGLE, { x: 4.7, y: 1.56, w: 1.4, h: 0.05, fill: { color: theme.accent } });
  }

  // 3 个关键指标卡（横排）
  if (metrics && metrics.length > 0) {
    const cardW = 1.52, cardH = 1.55, cardY = 1.82, gap = 0.1;
    metrics.slice(0, 3).forEach((m, i) => {
      const cx = 4.7 + i * (cardW + gap);
      // 卡片背景
      slide.addShape(pres.shapes.RECTANGLE, { x: cx, y: cardY, w: cardW, h: cardH, fill: { color: theme.light }, line: { color: theme.border, width: 0.5 } });
      // 顶部橙色条
      slide.addShape(pres.shapes.RECTANGLE, { x: cx, y: cardY, w: cardW, h: 0.06, fill: { color: i === 0 ? theme.accent : theme.secondary } });
      // 数值
      slide.addText(m.value, { x: cx + 0.06, y: cardY + 0.12, w: cardW - 0.12, h: 0.78, fontSize: 34, fontFace: "Arial Black", color: i === 0 ? theme.accent : theme.secondary, bold: true, align: "center", valign: "middle", margin: 0 });
      // 单位
      if (m.unit) {
        slide.addText(m.unit, { x: cx + cardW * 0.55, y: cardY + 0.16, w: cardW * 0.42, h: 0.22, fontSize: 10, fontFace: "Microsoft YaHei", color: i === 0 ? theme.accent : theme.secondary, bold: true, align: "left", valign: "top", margin: 0 });
      }
      // 标签
      slide.addText(m.label, { x: cx + 0.06, y: cardY + 0.94, w: cardW - 0.12, h: 0.52, fontSize: 10, fontFace: "Microsoft YaHei", color: theme.primary, bold: true, align: "center", valign: "middle", margin: 0, lineSpaceMult: 1.2 });
    });
  }

  // 底部价值标语条（右侧）
  slide.addShape(pres.shapes.RECTANGLE, { x: 4.7, y: 4.72, w: 5.0, h: 0.62, fill: { color: theme.light } });
  slide.addShape(pres.shapes.RECTANGLE, { x: 4.7, y: 4.72, w: 0.06, h: 0.62, fill: { color: theme.accent } });
  slide.addText("以技术驱动价值，以数据创造洞察", { x: 4.82, y: 4.72, w: 4.8, h: 0.62, fontSize: 11, fontFace: "Microsoft YaHei", color: theme.primary, align: "left", valign: "middle", margin: 0 });

  return slide;
}
```

**调用示例：**
```javascript
createRichCover(pres, theme,
  "AI 智能运营平台",           // title
  "赋能医疗机构数字化转型",     // subtitle
  "解决方案 · 2025",           // tag
  "2025年 04月",               // dateStr
  [
    { value: "95%", unit: "+", label: "慢病随访\n完成率" },
    { value: "1.18", unit: "亿", label: "覆盖空巢\n老人规模" },
    { value: "40%", unit: "↓", label: "运营成本\n降幅" },
  ],
  "让每一次随访都精准有效，\n让每一条数据都产生价值"  // valueSlogan
);
```

### TOC（目录）

左侧深蓝色带 + 橙色圆形章节编号 + 右侧章节列表。

```javascript
function createHuaweiTOCSlide(pres, theme, chapters, slideNum) {
  // chapters: [{ title, desc? }]
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧深蓝色带
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 2.0, h: 5.625,
    fill: { color: theme.primary }
  });
  // 橙色细竖线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 2.0, y: 0, w: 0.07, h: 5.625,
    fill: { color: theme.accent }
  });
  // "目录" 标签
  slide.addText("目录", {
    x: 0.1, y: 2.0, w: 1.8, h: 0.65,
    fontSize: 26, fontFace: "Microsoft YaHei", color: theme.headerText,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  slide.addText("CONTENTS", {
    x: 0.1, y: 2.72, w: 1.8, h: 0.28,
    fontSize: 10, fontFace: "Arial", color: theme.light,
    align: "center", margin: 0
  });
  // 橙色短横线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.55, y: 1.82, w: 0.9, h: 0.05,
    fill: { color: theme.accent }
  });

  // 章节列表
  const startY = 0.55;
  const itemH = Math.min(0.88, 4.3 / Math.max(chapters.length, 1));

  chapters.forEach((ch, i) => {
    const cy = startY + i * itemH;
    const circY = cy + (itemH - 0.44) / 2;

    // 橙色圆形序号
    slide.addShape(pres.shapes.OVAL, {
      x: 2.3, y: circY, w: 0.44, h: 0.44,
      fill: { color: theme.accent }
    });
    slide.addText(String(i + 1).padStart(2, '0'), {
      x: 2.3, y: circY, w: 0.44, h: 0.44,
      fontSize: 12, fontFace: "Arial Black", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    // 连接细线
    slide.addShape(pres.shapes.LINE, {
      x: 2.88, y: circY + 0.22, w: 0.2, h: 0,
      line: { color: theme.accent, width: 0.75 }
    });
    // 章节标题
    slide.addText(ch.title, {
      x: 3.18, y: cy + (itemH - (ch.desc ? 0.75 : 0.42)) / 2,
      w: 6.4, h: 0.42,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    if (ch.desc) {
      slide.addText(ch.desc, {
        x: 3.18, y: cy + (itemH - 0.75) / 2 + 0.44,
        w: 6.4, h: 0.32,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.mutedText, align: "left", margin: 0
      });
    }
    // 分隔线
    if (i < chapters.length - 1) {
      slide.addShape(pres.shapes.LINE, {
        x: 2.3, y: cy + itemH - 0.05, w: 7.2, h: 0,
        line: { color: theme.border, width: 0.4 }
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### Section Divider（章节分隔页）

见上方「标志性设计元素 §7」的 `createHuaweiSectionDivider`。

### Content（内容页）

标准四栏 / 三栏 / 两栏布局，全部搭配 `addHuaweiSlideTitle` 标题栏。

**两栏布局（左文字/要点 + 右图表/架构）：**

```javascript
function createTwoColumnSlide(pres, theme, title, moduleTag, leftContent, rightContent, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addHuaweiSlideTitle(slide, pres, theme, title, moduleTag, source);

  // 中间分隔线
  slide.addShape(pres.shapes.LINE, {
    x: 4.92, y: 1.1, w: 0, h: 4.0,
    line: { color: theme.border, width: 0.6 }
  });

  // 左侧：要点列表区（x: 0.4, w: 4.3）
  // 右侧：图表/架构区（x: 5.1, w: 4.5）
  // 由调用方根据具体内容填充两侧内容

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**三栏等宽卡片布局：**

```javascript
function createThreeCardSlide(pres, theme, title, moduleTag, cards, source, slideNum) {
  // cards: [{ num, title, desc, highlight? }]  最多 3 张
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addHuaweiSlideTitle(slide, pres, theme, title, moduleTag, source);

  const cardW = 2.87, cardH = 3.8, startX = 0.4, gap = 0.145;

  cards.slice(0, 3).forEach((card, i) => {
    addHuaweiNumberedCard(
      slide, pres, theme,
      startX + i * (cardW + gap), 1.1,
      cardW, cardH,
      card.num || i + 1,
      card.title,
      card.desc,
      card.highlight || false
    );
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**KPI 数据总览页（4 个 KPI + 说明文字）：**

```javascript
function createKpiOverviewSlide(pres, theme, title, moduleTag, kpis, summary, source, slideNum) {
  // kpis: [{ value, unit?, label, desc?, useOrange? }]  最多 4 个
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addHuaweiSlideTitle(slide, pres, theme, title, moduleTag, source);

  const kpiW = 2.1, kpiH = 1.85;
  const startX = 0.4;

  kpis.slice(0, 4).forEach((kpi, i) => {
    addHuaweiKpiCard(
      slide, pres, theme,
      startX + i * (kpiW + 0.15), 1.1,
      kpiW, kpiH,
      kpi.value, kpi.unit, kpi.label, kpi.desc,
      kpi.useOrange || false
    );
  });

  // 下方说明文字区
  if (summary) {
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 0.4, y: 3.1, w: 9.2, h: 1.9,
      fill: { color: theme.light },
      line: { color: theme.border, width: 0.5 }
    });
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 0.4, y: 3.1, w: 0.06, h: 1.9,
      fill: { color: theme.secondary }
    });
    slide.addText(summary, {
      x: 0.6, y: 3.15, w: 8.9, h: 1.8,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.bodyText, align: "left", valign: "top", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### Closing（结尾/感谢页）

深蓝全屏背景 + 居中橙色装饰 + 核心联系信息。

```javascript
function createHuaweiClosingSlide(pres, theme, mainText, contactInfo) {
  const slide = pres.addSlide();
  slide.background = { color: theme.primary };

  // 橙色中央横线（上）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 3.5, y: 1.8, w: 3.0, h: 0.07,
    fill: { color: theme.accent }
  });
  // 主文字
  slide.addText(mainText || "感谢您的聆听", {
    x: 1.0, y: 2.0, w: 8.0, h: 1.0,
    fontSize: 32, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 橙色中央横线（下）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 3.5, y: 3.1, w: 3.0, h: 0.07,
    fill: { color: theme.accent }
  });
  // 联系信息
  if (contactInfo) {
    slide.addText(contactInfo, {
      x: 1.0, y: 3.35, w: 8.0, h: 0.5,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.light, align: "center", margin: 0
    });
  }
  return slide;
}
```
