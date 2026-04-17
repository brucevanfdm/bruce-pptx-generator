# Style Preset: Pitch Deck（路演风）

适合场景：融资路演、产品 Roadmap 向上汇报、Business Case 提案、跨部门拉通。目标是让受众相信你、支持你。

## 氛围

**卖动** — 麦肯锡让人信服于逻辑，Pitch Deck 让人兴奋于可能性。每一页都在回答：为什么要支持这件事？数字要大，主张要清晰，故事弧线要有节奏。

## 默认叙事骨架

Pitch Deck 默认要比企业汇报更有推进感，推荐顺序：

1. Problem：痛点真实且足够大
2. Why Now：窗口期、技术条件、市场变化
3. Product：你到底做了什么
4. Traction：已经跑出来了什么
5. GTM / Moat：为什么你能继续赢
6. Ask：希望对方给什么支持

前半段卖“问题成立”，中段卖“你做得出来”，后半段卖“现在值得下注”。

## 签名页

这套风格的 signature pages 应优先是：

- **Traction Wall**：3–5 个关键数字 + 增长趋势 + 时间语境
- **Why Now Slide**：市场窗口、技术成熟度、政策或需求转折
- **Milestone Timeline**：已经做到哪、下一步去哪
- **Ask / Use of Funds / CTA Slide**：明确希望拿到的支持

如果没有一张强势 traction 页和一张清晰 CTA 页，Pitch Deck 通常不够“卖动”。

## 禁用模式

- 禁止把 Pitch Deck 写成普通产品说明书。不是“功能一二三”，而是“为什么值得支持”。
- 禁止大量长段落和背景介绍连续出现；每页都应推动读者往下翻。
- 禁止把预测当 traction。预测可以有，但必须和真实进展分开展示。
- 禁止结尾只是总结。最后一页必须是明确的 ask、试点邀请或决策请求。

## 图表与图形语法

- 图表优先回答“增长是否真实”“窗口是否存在”“资源投进去是否值得”。
- 优先使用 **traction KPI / growth chart / milestone timeline / market funnel / competitor matrix**。
- 里程碑、客户 logo、案例证据比复杂分析框架更符合这套风格。
- 每张数据页尽量带“时间轴”或“变化箭头”，强化向前推进感。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深夜蓝 | `0F172A` | 标题、主要文字 |
| `secondary` | 靛蓝 | `6366F1` | 强调色、高亮数字、标签 |
| `accent` | 琥珀橙 | `F59E0B` | CTA、警示、对比强调 |
| `light` | 冷白 | `F1F5F9` | 卡片背景、浅色区块 |
| `bg` | 纯白 | `FFFFFF` | 内容页背景 |
| `dividerBg` | 深夜蓝 | `0F172A` | 暗色章节页背景 |
| `bodyText` | 深板岩 | `1E293B` | 正文段落 |
| `mutedText` | 板岩灰 | `64748B` | 次级文字、说明 |
| `border` | 浅板岩 | `E2E8F0` | 卡片边框、分隔线 |

```javascript
const theme = {
  primary:   "0F172A",
  secondary: "6366F1",
  accent:    "F59E0B",
  light:     "F1F5F9",
  bg:        "FFFFFF",
  dividerBg: "0F172A",
  bodyText:  "1E293B",
  mutedText: "64748B",
  border:    "E2E8F0",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 40–50 | Bold | `primary` |
| 封面 Tagline | Microsoft YaHei | 18–22 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 26–32 | Bold | `primary` |
| 章节页标题 | Microsoft YaHei | 36–44 | Bold | `FFFFFF` |
| 二级标题 / 卡片标题 | Microsoft YaHei | 15–18 | Bold | `primary` |
| 正文 | Microsoft YaHei | 12–14 | Regular | `bodyText` |
| 说明 / 注释 | Microsoft YaHei | 10–12 | Regular | `mutedText` |
| 核心数字（Traction） | Arial Black | 52–72 | Bold | `secondary` |
| 次级数字 | Arial Black | 32–44 | Bold | `primary` |
| 标签文字 | Microsoft YaHei | 11–13 | Bold | `FFFFFF`（深色底） |

## 布局网格系统

幻灯片尺寸 10" × 5.625"。

**安全边界：**
- 左/右边距：`0.5"`
- 上边距：`1.1"`（标题区以下）
- 下边距：`0.4"`
- 内容安全区：`x: 0.5–9.5`, `y: 1.1–5.2`

**Pitch Deck 特有结构规范：**
- 前 3 页必须回答：是什么 / 为什么现在 / 你是谁
- 每页有明确的"推进力"——读者看完这页应该更想往下看
- 数字必须是 Traction（真实进展），不是假设预测
- 最后一页必须有 CTA（下一步行动）

**内容密度指引（说服驱动型 — 精装标准）：**

> 本风格定位为**说服驱动型**：每张幻灯片一个核心主张，用数字和简洁支撑点证明它。

- 每张内容页：1 个核心主张 + **3–5 个支撑点**（每点需 tagline + 数据支撑）
- **Traction 页：3–5 个大数字，每个配简短标签 + 趋势箭头 + 底部洞察说明**
- 禁止长段落——超过 2 行的文字必须拆成带前缀的要点列表
- **每张内容页至少包含 1 种非文字视觉**（进度环 / 数据条 / 里程碑图 / KPI 卡）

## 标志性设计元素

### 1. 内容页标题（左侧靛蓝竖条）

Pitch Deck 标志性元素：左侧 4px 靛蓝竖线，强调主张。

```javascript
function addPitchSlideTitle(slide, pres, theme, title) {
  // 左侧靛蓝竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.5, y: 0.18, w: 0.07, h: 0.65,
    fill: { color: theme.secondary }
  });
  // 标题
  slide.addText(title, {
    x: 0.68, y: 0.18, w: 8.82, h: 0.65,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });
}
```



### 1.5 精装能力卡片（Rich Card）—— 推荐默认使用

**优先使用此组件替代基础的 `addTractionCard` + `addPitchBullets` 组合**。精装卡片包含：顶部强调色条、KPI 大数值、单位、tagline、带前缀的 bullet 列表、底部洞察说明区。

```javascript
function addPitchRichCard(slide, pres, theme, x, y, w, h, value, unit, label, tagline, features, detail, highlight) {
  const accentColor = highlight ? theme.accent : theme.secondary;
  const bgColor = highlight ? "FEF3C7" : theme.light; // 高亮用浅琥珀（配accent F59E0B），普通用冷白

  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h, fill: { color: bgColor }, line: { color: theme.border, width: 0.5 } });
  // 顶部强调色条
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h: 0.07, fill: { color: accentColor } });

  // KPI 大数值
  slide.addText(value, { x: x + 0.1, y: y + 0.18, w: w - 0.2, h: 0.72, fontSize: 40, fontFace: "Arial Black", color: accentColor, bold: true, align: "center", valign: "middle", margin: 0 });
  if (unit) {
    slide.addText(unit, { x: x + w * 0.52, y: y + 0.22, w: w * 0.45, h: 0.26, fontSize: 11, fontFace: "Microsoft YaHei", color: accentColor, bold: true, align: "left", valign: "top", margin: 0 });
  }

  // 标签
  slide.addText(label, { x: x + 0.1, y: y + 0.94, w: w - 0.2, h: 0.3, fontSize: 12, fontFace: "Microsoft YaHei", color: theme.primary, bold: true, align: "center", margin: 0 });

  // Tagline
  slide.addText(tagline, { x: x + 0.1, y: y + 1.26, w: w - 0.2, h: 0.28, fontSize: 9.5, fontFace: "Microsoft YaHei", color: accentColor, align: "center", margin: 0 });

  // 分隔线
  slide.addShape(pres.shapes.LINE, { x: x + 0.1, y: y + 1.6, w: w - 0.2, h: 0, line: { color: theme.border, width: 0.5 } });

  // Bullet 功能列表（带小方块前缀）
  const featStartY = y + 1.68;
  const featH = 0.4;
  features.forEach((f, i) => {
    const fy = featStartY + i * featH;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.12, y: fy + 0.13, w: 0.1, h: 0.1, fill: { color: accentColor } });
    slide.addText(f, { x: x + 0.28, y: fy + 0.06, w: w - 0.42, h: featH - 0.12, fontSize: 9.5, fontFace: "Microsoft YaHei", color: theme.bodyText, align: "left", valign: "middle", margin: 0 });
  });

  // 底部洞察说明区
  if (detail) {
    const footerY = y + h - 0.55;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.1, y: footerY, w: w - 0.2, h: 0.45, fill: { color: "FFFFFF" }, line: { color: theme.border, width: 0.3 } });
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.1, y: footerY, w: 0.05, h: 0.45, fill: { color: theme.mutedText } });
    slide.addText(detail, { x: x + 0.2, y: footerY, w: w - 0.38, h: 0.45, fontSize: 8.5, fontFace: "Microsoft YaHei", color: theme.mutedText, align: "left", valign: "middle", margin: 0 });
  }
}
```

### 2. 页码徽章

```javascript
function addPageBadge(slide, pres, theme, num) {
  // 胶囊形，靛蓝底
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 9.1, y: 5.18, w: 0.55, h: 0.28,
    fill: { color: theme.secondary },
    rectRadius: 0.14
  });
  slide.addText(String(num), {
    x: 9.1, y: 5.18, w: 0.55, h: 0.28,
    fontSize: 11, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. Traction 数字卡（核心 Metric）

```javascript
function addTractionCard(slide, pres, theme, x, y, w, value, label, growth) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 1.7,
    fill: { color: theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 顶部靛蓝细线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.06,
    fill: { color: theme.secondary }
  });
  // 核心数字
  slide.addText(value, {
    x: x + 0.1, y: y + 0.15, w: w - 0.2, h: 0.85,
    fontSize: 56, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + 1.05, w: w - 0.2, h: 0.3,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, bold: true,
    align: "center", margin: 0
  });
  // 增长标注（可选，琥珀橙）
  if (growth) {
    slide.addText(growth, {
      x: x + 0.1, y: y + 1.38, w: w - 0.2, h: 0.26,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.accent, bold: true,
      align: "center", margin: 0
    });
  }
}
```

### 4. 章节分隔页（全暗底 + 白色大主张）

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 靛蓝胶囊标签（章节编号）
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 0.5, y: 1.1, w: 0.95, h: 0.42,
    fill: { color: theme.secondary },
    rectRadius: 0.21
  });
  slide.addText(String(num).padStart(2, '0'), {
    x: 0.5, y: 1.1, w: 0.95, h: 0.42,
    fontSize: 16, fontFace: "Arial Black", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });

  // 主标题（白色大字）
  slide.addText(title, {
    x: 0.5, y: 1.7, w: 9.0, h: 1.6,
    fontSize: 40, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });

  // 副标题
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.5, y: 3.5, w: 7.0, h: 0.45,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 5. 要点列表（带靛蓝方块）

```javascript
function addPitchBullets(slide, pres, theme, x, y, w, items) {
  // items: [{ text, sub }]  sub 是可选的灰色说明
  let curY = y;
  items.forEach(item => {
    // 靛蓝方块
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: curY + 0.1, w: 0.1, h: 0.1,
      fill: { color: theme.secondary }
    });
    // 主文字
    slide.addText(item.text, {
      x: x + 0.2, y: curY, w: w - 0.2, h: 0.34,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.bodyText, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    curY += 0.34;
    if (item.sub) {
      slide.addText(item.sub, {
        x: x + 0.2, y: curY, w: w - 0.2, h: 0.26,
        fontSize: 11, fontFace: "Microsoft YaHei",
        color: theme.mutedText,
        align: "left", valign: "top", margin: 0
      });
      curY += 0.3;
    }
    curY += 0.12;
  });
}
```

### 6. 图表（增长叙事）

```javascript
/**
 * 基础图表函数：统一 Pitch Deck 图表样式
 * @param {object} slide - pptxgenjs slide 对象
 * @param {object} pres  - pptxgenjs 实例
 * @param {object} theme - 色板对象
 * @param {string} type  - 图表类型（如 pres.charts.LINE）
 * @param {Array}  chartData - [{ name, labels, values }]
 * @param {object} opts  - 附加配置（会合并到图表选项）
 */
function addPitchChart(slide, pres, theme, type, chartData, opts) {
  // 多系列时显示图例
  const showLegend = chartData.length > 1;

  const baseOpts = {
    // 图表区域白色背景
    chartArea: { fill: { color: "FFFFFF" } },
    // 系列颜色：靛蓝、琥珀橙、浅紫、浅琥珀
    chartColors: ["6366F1", "F59E0B", "818CF8", "FCD34D"],
    // 坐标轴标签颜色使用 mutedText
    catAxisLabelColor: theme.mutedText,
    valAxisLabelColor: theme.mutedText,
    // 数值网格线使用 border 颜色
    valGridLine: { color: theme.border, style: "solid", size: 0.5 },
    // 类别轴网格线隐藏
    catGridLine: { style: "none" },
    // 显示数值标签
    showValue: true,
    dataLabelColor: theme.bodyText,
    dataLabelFontSize: 10,
    // 图例（多系列时显示）
    showLegend,
    legendPos: "b",
    legendFontSize: 10,
    legendColor: theme.mutedText,
  };

  slide.addChart(type, chartData, { ...baseOpts, ...opts });
}
```

**用法示例：**

```javascript
addPitchChart(slide, pres, theme, pres.charts.LINE,
  [{ name: "ARR", labels: ["Q1","Q2","Q3","Q4"], values: [120,210,380,620] }],
  { x: 0.5, y: 1.1, w: 9.0, h: 3.8 }
);
```

```javascript
/**
 * 增长趋势叙事页：折线图 + 可选里程碑标注
 * @param {object} pres       - pptxgenjs 实例
 * @param {object} theme      - 色板对象
 * @param {string} title      - 幻灯片标题
 * @param {Array}  chartData  - [{ name, labels, values }]
 * @param {Array}  milestones - [{ x: 0~1比例, label }]，可为 null
 * @param {string} source     - 数据来源说明（可为 null）
 * @param {number} slideNum   - 页码
 */
function createGrowthChartSlide(pres, theme, title, chartData, milestones, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 标题
  addPitchSlideTitle(slide, pres, theme, title);

  // 里程碑标注区域高度：有里程碑时图表留出底部空间
  const chartH = milestones && milestones.length ? 3.2 : 3.8;

  // 全宽折线图
  addPitchChart(slide, pres, theme, pres.charts.LINE, chartData, {
    x: 0.5, y: 1.1, w: 9.0, h: chartH,
    lineSmooth: true,
    lineSize: 3,
  });

  // 里程碑标注（图表下方，琥珀橙方块 + 文字）
  if (milestones && milestones.length) {
    const timelineY = 1.1 + chartH + 0.08; // 紧贴图表下方
    const chartW = 9.0;

    milestones.forEach(m => {
      // x 位置按比例映射到图表宽度
      const dotX = 0.5 + m.x * chartW - 0.06;

      // 琥珀橙小方块
      slide.addShape(pres.shapes.RECTANGLE, {
        x: dotX, y: timelineY, w: 0.12, h: 0.12,
        fill: { color: theme.accent }
      });

      // 里程碑文字（居中于方块）
      slide.addText(m.label, {
        x: dotX - 0.5, y: timelineY + 0.14, w: 1.12, h: 0.26,
        fontSize: 9, fontFace: "Microsoft YaHei",
        color: theme.mutedText,
        align: "center", valign: "top", margin: 0
      });
    });
  }

  // 数据来源
  if (source) {
    slide.addText(`来源：${source}`, {
      x: 0.5, y: 5.28, w: 7.0, h: 0.22,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**用法示例：**

```javascript
createGrowthChartSlide(
  pres, theme,
  "ARR 连续 4 季度翻倍增长",
  [{ name: "ARR（万元）", labels: ["Q1","Q2","Q3","Q4"], values: [120, 260, 510, 980] }],
  [
    { x: 0.25, label: "产品上线" },
    { x: 0.5,  label: "完成 Pre-A" },
    { x: 0.75, label: "拓展企业客户" },
  ],
  "公司内部财务数据",
  5
);
```

### 7. SVG 内联图形（零依赖，完全同步）

```javascript
/**
 * 将 SVG 字符串转为 base64 data URI，供 slide.addImage({ data }) 使用
 * @param {string} svgStr - SVG 源代码字符串
 * @returns {string} base64 data URI
 */
function svgToBase64(svgStr) {
  // Node.js 环境使用 Buffer，浏览器环境使用 btoa
  if (typeof Buffer !== "undefined") {
    return "data:image/svg+xml;base64," + Buffer.from(svgStr).toString("base64");
  }
  return "data:image/svg+xml;base64," + btoa(unescape(encodeURIComponent(svgStr)));
}
```

```javascript
/**
 * TAM / SAM / SOM 市场漏斗 SVG
 * @param {Array}  stages - [{ label, value, color? }]，从大到小排列
 * @param {number} w      - SVG 宽度（px），默认 420
 * @param {number} h      - SVG 高度（px），默认 300
 * @returns {string} base64 data URI
 *
 * 默认颜色从深到浅：0F172A → 6366F1 → 818CF8
 */
function makeMarketFunnel(stages, w = 420, h = 300) {
  // 默认颜色梯度
  const defaultColors = ["0F172A", "6366F1", "818CF8", "A5B4FC"];
  const layerH = h / stages.length;
  // 漏斗最大半宽、最小半宽
  const maxHalfW = w * 0.42;
  const minHalfW = w * 0.14;
  const cx = w * 0.42; // 漏斗中心 x（留右侧空间标注）

  let shapePaths = "";
  let labels = "";

  stages.forEach((stage, i) => {
    const color = stage.color || defaultColors[i] || "6366F1";
    const topRatio = 1 - (i / stages.length);
    const botRatio = 1 - ((i + 1) / stages.length);
    const topHW = minHalfW + (maxHalfW - minHalfW) * topRatio;
    const botHW = minHalfW + (maxHalfW - minHalfW) * botRatio;
    const y1 = i * layerH;
    const y2 = (i + 1) * layerH;

    // 梯形路径
    shapePaths += `<polygon points="${cx - topHW},${y1} ${cx + topHW},${y1} ${cx + botHW},${y2} ${cx - botHW},${y2}" fill="#${color}" opacity="0.95"/>`;

    // 层内标签（白色）
    const midY = (y1 + y2) / 2;
    labels += `<text x="${cx}" y="${midY - 6}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="13" font-weight="bold" fill="#FFFFFF">${stage.label}</text>`;

    // 右侧金额标注
    const annotX = cx + topHW + 18;
    labels += `<text x="${annotX}" y="${midY + 5}" font-family="Arial Black,Arial,sans-serif" font-size="14" font-weight="bold" fill="#${color}">${stage.value}</text>`;

    // 连接线（从层中点到标注）
    labels += `<line x1="${cx + topHW}" y1="${midY}" x2="${annotX - 4}" y2="${midY}" stroke="#${color}" stroke-width="1.2" stroke-dasharray="4,3"/>`;
  });

  const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="${w}" height="${h}" viewBox="0 0 ${w} ${h}">
  <rect width="${w}" height="${h}" fill="#FFFFFF"/>
  ${shapePaths}
  ${labels}
</svg>`;

  return svgToBase64(svg);
}
```

**用法示例：**

```javascript
const funnel = makeMarketFunnel([
  { label: "TAM 总市场", value: "¥850亿" },
  { label: "SAM 可服务市场", value: "¥120亿" },
  { label: "SOM 可获取份额", value: "¥15亿" },
]);
slide.addImage({ data: funnel, x: 0.5, y: 1.1, w: 4.0, h: 3.5 });
```

```javascript
/**
 * 项目路线图时间轴 SVG
 * @param {Array}  milestones - [{ date, title, desc?, done?, current? }]
 * @param {number} w          - SVG 宽度（px），默认 860
 * @param {number} h          - SVG 高度（px），默认 160
 * @returns {string} base64 data URI
 *
 * 完成节点：靛蓝实心（6366F1）
 * 当前节点：琥珀橙高亮（F59E0B）+ 外环
 * 未来节点：空心圆（E2E8F0 边框）
 */
function makeRoadmapTimeline(milestones, w = 860, h = 160) {
  const n = milestones.length;
  const lineY = h * 0.42;       // 时间轴 Y
  const padX = 40;               // 左右内边距
  const usableW = w - padX * 2;
  const step = n > 1 ? usableW / (n - 1) : 0;

  // 背景水平线
  let lines = `<line x1="${padX}" y1="${lineY}" x2="${w - padX}" y2="${lineY}" stroke="#E2E8F0" stroke-width="3"/>`;

  // 完成段（已完成节点间填充靛蓝线）
  const doneIdxs = milestones.reduce((acc, m, i) => (m.done || m.current ? [...acc, i] : acc), []);
  if (doneIdxs.length > 1) {
    const x1 = padX + doneIdxs[0] * step;
    const x2 = padX + doneIdxs[doneIdxs.length - 1] * step;
    lines += `<line x1="${x1}" y1="${lineY}" x2="${x2}" y2="${lineY}" stroke="#6366F1" stroke-width="3"/>`;
  }

  let nodes = "";
  let texts = "";

  milestones.forEach((m, i) => {
    const cx = padX + i * step;

    if (m.current) {
      // 当前节点：琥珀橙实心 + 外环
      nodes += `<circle cx="${cx}" cy="${lineY}" r="13" fill="#FEF3C7" stroke="#F59E0B" stroke-width="2.5"/>`;
      nodes += `<circle cx="${cx}" cy="${lineY}" r="7" fill="#F59E0B"/>`;
    } else if (m.done) {
      // 已完成节点：靛蓝实心
      nodes += `<circle cx="${cx}" cy="${lineY}" r="8" fill="#6366F1"/>`;
      // 完成勾
      nodes += `<polyline points="${cx - 4},${lineY} ${cx - 1},${lineY + 4} ${cx + 5},${lineY - 4}" fill="none" stroke="#FFFFFF" stroke-width="2" stroke-linecap="round"/>`;
    } else {
      // 未来节点：空心圆
      nodes += `<circle cx="${cx}" cy="${lineY}" r="8" fill="#FFFFFF" stroke="#E2E8F0" stroke-width="2.5"/>`;
    }

    // 日期（节点上方）
    texts += `<text x="${cx}" y="${lineY - 22}" text-anchor="middle" font-family="Arial,sans-serif" font-size="11" fill="#64748B">${m.date}</text>`;

    // 标题（节点下方）
    const titleColor = m.current ? "F59E0B" : m.done ? "6366F1" : "64748B";
    texts += `<text x="${cx}" y="${lineY + 26}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="12" font-weight="bold" fill="#${titleColor}">${m.title}</text>`;

    // 描述（可选，更小字体）
    if (m.desc) {
      texts += `<text x="${cx}" y="${lineY + 44}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="10" fill="#94A3B8">${m.desc}</text>`;
    }
  });

  const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="${w}" height="${h}" viewBox="0 0 ${w} ${h}">
  <rect width="${w}" height="${h}" fill="#FFFFFF"/>
  ${lines}
  ${nodes}
  ${texts}
</svg>`;

  return svgToBase64(svg);
}
```

**用法示例：**

```javascript
const roadmap = makeRoadmapTimeline([
  { date: "2024 Q1", title: "MVP 上线", done: true },
  { date: "2024 Q3", title: "首批客户", done: true },
  { date: "2025 Q1", title: "Pre-A 融资", current: true },
  { date: "2025 Q3", title: "规模化增长" },
  { date: "2026 Q1", title: "Series A" },
]);
slide.addImage({ data: roadmap, x: 0.5, y: 1.5, w: 9.0, h: 1.8 });
```

```javascript
/**
 * 竞争定位 2×2 矩阵 SVG
 * @param {Array}  quadrants - 4 个象限，顺序：[左上, 右上, 左下, 右下]
 *                             每项 { label, sublabel?, color? }
 * @param {string} xAxis     - X 轴标签（从左到右）
 * @param {string} yAxis     - Y 轴标签（从下到上）
 * @param {number} w         - SVG 宽度（px），默认 440
 * @param {number} h         - SVG 高度（px），默认 380
 * @returns {string} base64 data URI
 *
 * 高亮象限（右上，index 1）用 6366F1，其余用 F1F5F9
 */
function makeCompetitorMatrix(quadrants, xAxis, yAxis, w = 440, h = 380) {
  // 矩阵区域边界
  const ml = 52, mr = 20, mt = 20, mb = 52;
  const mw = w - ml - mr;
  const mh = h - mt - mb;
  const cx = ml + mw / 2;  // 中心 x
  const cy = mt + mh / 2;  // 中心 y

  // 象限位置：[左上, 右上, 左下, 右下]
  const quadPos = [
    { x: ml,      y: mt,      w: mw / 2, h: mh / 2 },  // 左上 (index 0)
    { x: cx,      y: mt,      w: mw / 2, h: mh / 2 },  // 右上 (index 1) 高亮
    { x: ml,      y: cy,      w: mw / 2, h: mh / 2 },  // 左下 (index 2)
    { x: cx,      y: cy,      w: mw / 2, h: mh / 2 },  // 右下 (index 3)
  ];

  const defaultColors = ["F1F5F9", "6366F1", "F1F5F9", "F1F5F9"];
  const textColors    = ["1E293B", "FFFFFF", "1E293B", "1E293B"];

  let rects = "";
  let labels = "";

  quadrants.forEach((q, i) => {
    const pos = quadPos[i];
    const bg = q.color || defaultColors[i];
    const tc = i === 1 && !q.color ? textColors[1] : textColors[i] || "1E293B";

    // 象限背景
    rects += `<rect x="${pos.x}" y="${pos.y}" width="${pos.w}" height="${pos.h}" fill="#${bg}" stroke="#E2E8F0" stroke-width="1"/>`;

    // 象限主标签
    const labelX = pos.x + pos.w / 2;
    const labelY = pos.y + pos.h / 2 - (q.sublabel ? 10 : 0);
    labels += `<text x="${labelX}" y="${labelY}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="13" font-weight="bold" fill="#${tc}">${q.label}</text>`;

    // 副标签
    if (q.sublabel) {
      labels += `<text x="${labelX}" y="${labelY + 18}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="10" fill="#${tc}" opacity="0.8">${q.sublabel}</text>`;
    }
  });

  // 坐标轴箭头（X 轴）
  const axisColor = "94A3B8";
  const arrowX = `<line x1="${ml - 4}" y1="${h - mb}" x2="${w - mr}" y2="${h - mb}" stroke="#${axisColor}" stroke-width="2"/>
  <polygon points="${w - mr},${h - mb - 5} ${w - mr + 10},${h - mb} ${w - mr},${h - mb + 5}" fill="#${axisColor}"/>`;

  // 坐标轴箭头（Y 轴）
  const arrowY = `<line x1="${ml}" y1="${h - mb + 4}" x2="${ml}" y2="${mt}" stroke="#${axisColor}" stroke-width="2"/>
  <polygon points="${ml - 5},${mt} ${ml},${mt - 10} ${ml + 5},${mt}" fill="#${axisColor}"/>`;

  // 轴标签
  const axisLabels = `
  <text x="${w / 2}" y="${h - 6}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="12" fill="#64748B">${xAxis}</text>
  <text x="14" y="${h / 2}" text-anchor="middle" font-family="Microsoft YaHei,Arial,sans-serif" font-size="12" fill="#64748B" transform="rotate(-90, 14, ${h / 2})">${yAxis}</text>`;

  const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="${w}" height="${h}" viewBox="0 0 ${w} ${h}">
  <rect width="${w}" height="${h}" fill="#FFFFFF"/>
  ${rects}
  ${arrowX}
  ${arrowY}
  ${axisLabels}
  ${labels}
</svg>`;

  return svgToBase64(svg);
}
```

**用法示例：**

```javascript
const matrix = makeCompetitorMatrix(
  [
    { label: "传统供应商", sublabel: "功能全，价格高" },
    { label: "我们", sublabel: "智能化 + 低成本" },   // 右上高亮
    { label: "小工具", sublabel: "价格低，功能弱" },
    { label: "新兴竞品", sublabel: "智能化，价格高" },
  ],
  "价格竞争力",
  "智能化程度"
);
slide.addImage({ data: matrix, x: 5.2, y: 1.1, w: 4.3, h: 4.0 });
```

## 5 种页面类型

### Cover（封面）

白色背景，标题 + Tagline（靛蓝色）。右下角可放公司名或 Logo 占位。

```javascript
slide.background = { color: theme.bg };

slide.addText("项目 / 产品名", {
  x: 0.5, y: 1.2, w: 8.6, h: 1.5,
  fontSize: 48, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true,
  align: "left", margin: 0
});

slide.addText("一句话说清楚你要做什么", {
  x: 0.5, y: 2.9, w: 7.0, h: 0.6,
  fontSize: 20, fontFace: "Microsoft YaHei",
  color: theme.secondary, align: "left", margin: 0
});

slide.addText("2025  ·  产品部", {
  x: 0.5, y: 5.1, w: 4.0, h: 0.3,
  fontSize: 12, fontFace: "Microsoft YaHei",
  color: theme.mutedText, align: "left", margin: 0
});
```

### Cover 精装版（推荐默认使用）

**`createRichCover` — 路演封面精装版。** 右侧 3 个 Traction 数字用大字冲击，让投资人第一眼就感受到规模感。

```javascript
/**
 * @param {string} title      - 项目/产品名（大字，左对齐）
 * @param {string} tagline    - 一句话说清楚在做什么（靛蓝色）
 * @param {string} dateStr    - 日期/阶段/公司名
 * @param {Array}  traction   - 右侧 3 个牵引力数字，每项 { value, unit, label }
 *                              例：[{ value:"2.1万", unit:"", label:"付费用户" }, ...]
 * @param {string} stage      - 融资阶段标签（如"Pre-A 轮"），显示在右上角，可选
 */
function createRichCover(pres, theme, title, tagline, dateStr, traction, stage) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 顶部琥珀橙全宽强调线
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 0, w: 10, h: 0.06, fill: { color: theme.accent } });

  // 左侧：主标题
  slide.addText(title, {
    x: 0.5, y: 0.9, w: 5.6, h: 2.0,
    fontSize: 46, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "top", margin: 0, lineSpaceMult: 1.2
  });

  // Tagline
  if (tagline) {
    slide.addText(tagline, {
      x: 0.5, y: 3.1, w: 5.6, h: 0.62,
      fontSize: 18, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "left", margin: 0
    });
  }

  // 底部信息条
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 5.2, w: 10, h: 0.425, fill: { color: theme.primary } });
  slide.addText(dateStr || "", {
    x: 0.5, y: 5.2, w: 5.0, h: 0.425,
    fontSize: 11, fontFace: "Microsoft YaHei",
    color: "FFFFFF", align: "left", valign: "middle", margin: 0
  });

  // ── 右侧：3 个 Traction 数字 ──────────────────────────────
  if (stage) {
    // 融资阶段标签（右上角）
    slide.addShape(pres.shapes.RECTANGLE, { x: 7.6, y: 0.18, w: 2.1, h: 0.46, fill: { color: theme.secondary } });
    slide.addText(stage, { x: 7.6, y: 0.18, w: 2.1, h: 0.46, fontSize: 13, fontFace: "Microsoft YaHei", color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0 });
  }

  // 垂直分隔线
  slide.addShape(pres.shapes.RECTANGLE, { x: 6.5, y: 0.9, w: 0.04, h: 4.1, fill: { color: theme.border } });

  const cardY = [0.85, 2.32, 3.79];
  (traction || []).slice(0, 3).forEach((t, i) => {
    const cy = cardY[i];
    // 数字
    slide.addText(t.value, {
      x: 6.72, y: cy, w: 3.0, h: 1.0,
      fontSize: 52, fontFace: "Arial Black",
      color: i === 0 ? theme.accent : theme.secondary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    // 单位
    if (t.unit) {
      slide.addText(t.unit, { x: 8.0, y: cy + 0.08, w: 1.6, h: 0.38, fontSize: 16, fontFace: "Arial Black", color: theme.secondary, bold: true, align: "left", margin: 0 });
    }
    // 标签
    slide.addText(t.label, {
      x: 6.72, y: cy + 0.88, w: 3.0, h: 0.32,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
    // 细分隔线（最后一项不加）
    if (i < 2) {
      slide.addShape(pres.shapes.RECTANGLE, { x: 6.72, y: cy + 1.24, w: 2.8, h: 0.02, fill: { color: theme.border } });
    }
  });

  return slide;
}
```

**调用示例：**
```javascript
createRichCover(pres, theme,
  "智慧医疗\n随访平台",
  "让慢病管理像发消息一样简单",
  "2025年 04月  ·  健康科技",
  [
    { value: "2.1万", unit: "", label: "月活付费用户" },
    { value: "320%", unit: "", label: "环比年增长率" },
    { value: "87",   unit: "分", label: "用户 NPS 净推荐值" },
  ],
  "Pre-A 轮"
);
```

### TOC（目录）

```javascript
/**
 * 目录页：左侧深夜蓝 AGENDA 标题区 + 右侧章节列表
 * @param {object} pres     - pptxgenjs 实例
 * @param {object} theme    - 色板对象
 * @param {Array}  chapters - [{ title, desc }]，3–5 项
 * @param {number} slideNum - 页码
 */
function createTOCSlide(pres, theme, chapters, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧深夜蓝背景色块（AGENDA 标题区）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 2.5, h: 5.625,
    fill: { color: theme.primary }
  });

  // AGENDA 竖排大字
  slide.addText("AGENDA", {
    x: 0.08, y: 1.5, w: 2.35, h: 2.6,
    fontSize: 22, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "center", valign: "middle",
    charSpacing: 6,
    margin: 0
  });

  // 天蓝细竖线分隔
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 2.5, y: 0, w: 0.05, h: 5.625,
    fill: { color: theme.secondary }
  });

  // 右侧章节列表
  const listX = 2.72;
  const listW = 6.9;
  const startY = 0.65;
  const itemH = (5.625 - startY - 0.4) / (chapters.length || 1);

  chapters.forEach((ch, i) => {
    const itemY = startY + i * itemH;

    // 靛蓝圆角矩形序号
    slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
      x: listX, y: itemY + 0.08, w: 0.38, h: 0.38,
      fill: { color: theme.secondary },
      rectRadius: 0.08
    });
    slide.addText(String(i + 1).padStart(2, "0"), {
      x: listX, y: itemY + 0.08, w: 0.38, h: 0.38,
      fontSize: 12, fontFace: "Arial Black", color: "FFFFFF",
      bold: true, align: "center", valign: "middle", margin: 0
    });

    // 竖线分隔（序号与标题之间）
    slide.addShape(pres.shapes.RECTANGLE, {
      x: listX + 0.48, y: itemY + 0.1, w: 0.03, h: 0.34,
      fill: { color: theme.border }
    });

    // 章节标题
    slide.addText(ch.title, {
      x: listX + 0.62, y: itemY + 0.06, w: listW - 0.62, h: 0.26,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });

    // 章节描述
    if (ch.desc) {
      slide.addText(ch.desc, {
        x: listX + 0.62, y: itemY + 0.34, w: listW - 0.62, h: 0.22,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.mutedText,
        align: "left", valign: "top", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**用法示例：**

```javascript
createTOCSlide(pres, theme, [
  { title: "问题与机会", desc: "市场痛点及可服务规模" },
  { title: "产品解决方案", desc: "核心功能与差异化优势" },
  { title: "增长 Traction", desc: "关键数据与里程碑" },
  { title: "商业模式", desc: "收入来源与单位经济" },
  { title: "融资计划", desc: "本轮资金用途与目标" },
], 2);
```

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，全暗底 + 白色主张 + 章节标签。

### Content（内容页）

背景 `theme.bg`，标题用 `addPitchSlideTitle`，页码用 `addPageBadge`。

| 内容关系 | 布局 |
|----------|------|
| 核心 Traction 数据 | 横排 3–4 个 `addTractionCard` |
| 并列要点 / 证据 | `addPitchBullets`，配简短说明 |
| 问题 vs 方案 | 左右两栏，左红/右绿强调 |
| 路线图 / 时间线 | 横向时间轴，靛蓝节点 + 琥珀橙当前位置 |
| 竞争分析 | 象限图或对比表，用靛蓝标出我方优势 |
| 增长趋势叙事 | `createGrowthChartSlide`（LINE + 里程碑） |
| 市场规模拆解 | `makeMarketFunnel` SVG（TAM/SAM/SOM） |
| 产品路线图 | `makeRoadmapTimeline` SVG |
| 竞争定位分析 | `makeCompetitorMatrix` SVG |

### Summary（CTA 结尾页）

```javascript
/**
 * CTA 结尾页：深夜蓝背景 + 白色大字 headline + 琥珀橙分隔线 + ctaItems 列表
 * @param {object} pres      - pptxgenjs 实例
 * @param {object} theme     - 色板对象
 * @param {string} headline  - 白色大标题（"我们需要…" 格式）
 * @param {string} ask       - "我们的 Ask" 标签旁的简短说明（可为 null）
 * @param {Array}  ctaItems  - [{ text }]，2–3 条行动要点
 * @param {number} slideNum  - 页码
 */
function createCTASummarySlide(pres, theme, headline, ask, ctaItems, slideNum) {
  const slide = pres.addSlide();
  // 深夜蓝背景
  slide.background = { color: theme.dividerBg };

  // 靛蓝顶部装饰线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.1,
    fill: { color: theme.secondary }
  });

  // 白色大字 headline
  slide.addText(headline, {
    x: 0.5, y: 0.5, w: 9.0, h: 1.4,
    fontSize: 38, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });

  // 琥珀橙水平分隔线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.5, y: 2.1, w: 9.0, h: 0.04,
    fill: { color: theme.accent }
  });

  // 靛蓝圆角矩形"我们的 Ask"标签
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 0.5, y: 2.25, w: 1.6, h: 0.36,
    fill: { color: theme.secondary },
    rectRadius: 0.1
  });
  slide.addText("我们的 Ask", {
    x: 0.5, y: 2.25, w: 1.6, h: 0.36,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "center", valign: "middle", margin: 0
  });

  // Ask 简短说明
  if (ask) {
    slide.addText(ask, {
      x: 2.25, y: 2.3, w: 7.2, h: 0.28,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.mutedText,
      align: "left", valign: "middle", margin: 0
    });
  }

  // CTA 条目列表（琥珀橙方块编号 + 白色文字）
  const itemStartY = 2.82;
  const itemGap = 0.62;

  (ctaItems || []).forEach((item, i) => {
    const iy = itemStartY + i * itemGap;

    // 琥珀橙方块编号
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 0.5, y: iy, w: 0.36, h: 0.36,
      fill: { color: theme.accent }
    });
    slide.addText(String(i + 1), {
      x: 0.5, y: iy, w: 0.36, h: 0.36,
      fontSize: 14, fontFace: "Arial Black", color: "FFFFFF",
      bold: true, align: "center", valign: "middle", margin: 0
    });

    // 白色要点文字
    slide.addText(item.text, {
      x: 0.98, y: iy + 0.02, w: 8.55, h: 0.34,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: "FFFFFF",
      align: "left", valign: "middle", margin: 0
    });
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**用法示例：**

```javascript
createCTASummarySlide(
  pres, theme,
  "我们需要 1500 万完成规模化跨越",
  "本轮 Pre-A，用途明确，18 个月跑通盈利模型",
  [
    { text: "产品研发 × 500 万：完成企业级 SaaS 版本，支撑 100+ 客户并发" },
    { text: "市场拓展 × 600 万：华东 3 城 BD 团队，签约 50 家标杆客户" },
    { text: "运营储备 × 400 万：18 个月现金储备，覆盖 Break-even 节点" },
  ],
  12
);
```

## 视觉选择决策树

根据内容类型选择合适的视觉组件，避免全文字布局：

| 内容类型 | 推荐组件 |
|---------|---------|
| 核心增长数字（Traction） | `addTractionCard`（3–4 个横排） |
| 时间序列增长趋势 | `createGrowthChartSlide`（LINE + 里程碑） |
| 类别对比数据 | `addPitchChart(BAR)` |
| 市场规模拆解（TAM/SAM/SOM） | `makeMarketFunnel` SVG |
| 产品路线图 / 里程碑 | `makeRoadmapTimeline` SVG |
| 竞争定位 / 2×2 矩阵 | `makeCompetitorMatrix` SVG |
| 并列要点 / 证据支撑 | `addPitchBullets` |
| 章节导航 / 全局结构 | `createTOCSlide` |
| 章节切换 / 节奏制造 | `createSectionDividerSlide` |
| 融资 Ask / 行动号召 | `createCTASummarySlide` |

**每张 Content 页至少包含一种非纯文字的视觉组件（图表、SVG 图形），除非内容本身是纯文字分析结论。**

## Pitch Deck 专项规则

**叙事规则：**
- 故事弧线：痛点 → 机会 → 解决方案 → 证据（Traction）→ 团队 → Ask
- 每页标题是一个有立场的主张，不是中性描述
- Traction 数字必须真实，用 `growth` 字段标明增长方向

**视觉规则：**
- 靛蓝（`secondary`）用于"我们做到了"的正面强调
- 琥珀橙（`accent`）用于"紧迫性"和"行动"，不滥用
- 禁止超过 3 种强调色同时出现在一页
- 章节分隔页必须用暗底（制造节奏感）
