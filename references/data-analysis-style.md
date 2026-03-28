# Style Preset: 数据分析风（Data Analysis）

适合场景：用户研究汇报、A/B 测试结果、OKR 进展、指标 Review、数据驱动的产品决策会议。数据是主角，一切设计服务于数据的可读性。

## 氛围

**讲清** — 图表、表格、指标卡是核心载体。视觉设计退场，数据登场。让受众在 5 秒内找到关键数字，在 15 秒内理解结论。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深海蓝 | `0F2B46` | 标题、坐标轴、图表框架 |
| `secondary` | 数据蓝 | `1A7BC4` | 主数据系列、关键指标 |
| `accent` | 警示橙 | `E85D04` | 负向变化、风险、对比数据 |
| `light` | 冰蓝底 | `EBF4FF` | 表格斑马行、卡片底色 |
| `bg` | 纯白 | `FFFFFF` | 所有内容页背景 |
| `dividerBg` | 深海蓝 | `0F2B46` | 章节分隔页背景 |
| `bodyText` | 深蓝灰 | `1E3A5F` | 正文、标注 |
| `mutedText` | 板岩灰 | `64748B` | 坐标轴标签、说明、来源 |
| `positive` | 生长绿 | `16A34A` | 正向变化、达成指标 |
| `border` | 浅蓝灰 | `CBD5E1` | 表格边框、卡片边框 |

```javascript
const theme = {
  primary:   "0F2B46",
  secondary: "1A7BC4",
  accent:    "E85D04",
  light:     "EBF4FF",
  bg:        "FFFFFF",
  dividerBg: "0F2B46",
  bodyText:  "1E3A5F",
  mutedText: "64748B",
  positive:  "16A34A",
  border:    "CBD5E1",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 32–40 | Bold | `primary` |
| 内容页标题（结论句） | Microsoft YaHei | 22–26 | Bold | `primary` |
| 二级标题 / 图表标题 | Microsoft YaHei | 14–16 | Bold | `primary` |
| 正文 / 分析说明 | Microsoft YaHei | 11–13 | Regular | `bodyText` |
| 轴标签 / 图例 | Microsoft YaHei | 9–11 | Regular | `mutedText` |
| 来源 / 数据截止日 | Microsoft YaHei | 9–10 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 40–56 | Bold | `secondary` |
| 变化值（↑↓） | Arial Black | 18–24 | Bold | `positive` / `accent` |
| 表头 | Microsoft YaHei | 11–12 | Bold | `FFFFFF`（`primary` 底） |
| 表格内容 | Microsoft YaHei | 10–12 | Regular | `bodyText` |

> 数据分析风的字号整体偏小，为图表和表格留出更多空间。标题用结论句补偿信息密度。

## 布局网格系统

幻灯片尺寸 10" × 5.625"。

**安全边界：**
- 左/右边距：`0.4"`
- 上边距：`1.0"`（标题区以下）
- 下边距：`0.35"`（来源注释区）
- 内容安全区：`x: 0.4–9.6`, `y: 1.0–5.0`

**数据页专用布局规范：**
- 图表区：占页面 60%–70% 面积
- 分析说明区：右侧或下方，不超过 30% 面积
- 来源注释：左下角，`mutedText` 9pt
- 所有图表必须有标题（图表说明什么），不依赖听众自行解读

**内容密度指引（数据汇报型）：**

> 本风格定位为**数据汇报型**：每张幻灯片一个核心发现，用图表/表格证明，用一行文字点出结论。

- 每张内容页：1 个核心发现 + 1 个主图表/表格 + 1–3 行分析说明
- KPI 页：4–6 个指标，配变化趋势
- 对比页：2 组数据，明确标出差异
- 禁止在一页放两个以上图表（除非是同一指标的不同维度拆分）

## 标志性设计元素

### 1. 内容页标题（结论句 + 数据蓝下划线）

```javascript
function addDataSlideTitle(slide, pres, theme, title, source) {
  // 结论句标题
  slide.addText(title, {
    x: 0.4, y: 0.12, w: 9.2, h: 0.65,
    fontSize: 24, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 数据蓝全宽细线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.4, y: 0.82, w: 9.2, h: 0.03,
    fill: { color: theme.border }
  });
  // 左侧数据蓝强调段
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.4, y: 0.82, w: 1.2, h: 0.03,
    fill: { color: theme.secondary }
  });
  // 来源注释（左下角）
  if (source) {
    slide.addText(`数据来源：${source}`, {
      x: 0.4, y: 5.32, w: 6.0, h: 0.22,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }
}
```

### 2. 页码徽章

```javascript
function addPageBadge(slide, pres, theme, num) {
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 9.3, y: 5.2, w: 0.4, h: 0.28,
    fill: { color: theme.secondary }
  });
  slide.addText(String(num), {
    x: 9.3, y: 5.2, w: 0.4, h: 0.28,
    fontSize: 11, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. KPI 变化卡（带趋势标注）

```javascript
function addKPIChangeCard(slide, pres, theme, x, y, w, value, label, change, isPositive) {
  const changeColor = isPositive ? theme.positive : theme.accent;
  const changeSymbol = isPositive ? "↑" : "↓";

  // 卡片底色
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 1.65,
    fill: { color: theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 顶部数据蓝细线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.05,
    fill: { color: theme.secondary }
  });
  // 核心数值
  slide.addText(value, {
    x: x + 0.1, y: y + 0.1, w: w - 0.2, h: 0.85,
    fontSize: 48, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 变化值
  if (change) {
    slide.addText(`${changeSymbol} ${change}`, {
      x: x + 0.1, y: y + 0.98, w: w - 0.2, h: 0.3,
      fontSize: 20, fontFace: "Arial Black",
      color: changeColor, bold: true,
      align: "center", margin: 0
    });
  }
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + 1.32, w: w - 0.2, h: 0.28,
    fontSize: 11, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });
}
```

### 4. 数据表格（双色斑马行）

```javascript
function addDataTable(slide, pres, theme, x, y, w, h, headers, rows) {
  const colW = w / headers.length;
  const rowH = (h - 0.4) / rows.length;

  // 表头（深海蓝底）
  headers.forEach((header, i) => {
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + i * colW, y, w: colW, h: 0.4,
      fill: { color: theme.primary }
    });
    slide.addText(header, {
      x: x + i * colW + 0.08, y, w: colW - 0.16, h: 0.4,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: "FFFFFF", bold: true,
      align: i === 0 ? "left" : "center", valign: "middle", margin: 0
    });
  });

  // 数据行（斑马行：冰蓝 / 白）
  rows.forEach((row, ri) => {
    const rowY = y + 0.4 + ri * rowH;
    const isEven = ri % 2 === 0;
    row.forEach((cell, ci) => {
      if (isEven) {
        slide.addShape(pres.shapes.RECTANGLE, {
          x: x + ci * colW, y: rowY, w: colW, h: rowH,
          fill: { color: theme.light }
        });
      }
      // 数值列：检测是否含有正负符号自动着色
      const isChange = typeof cell === "string" && (cell.startsWith("↑") || cell.startsWith("↓"));
      const textColor = isChange
        ? (cell.startsWith("↑") ? theme.positive : theme.accent)
        : theme.bodyText;

      slide.addText(String(cell), {
        x: x + ci * colW + 0.08, y: rowY, w: colW - 0.16, h: rowH,
        fontSize: 11, fontFace: "Microsoft YaHei",
        color: textColor, bold: isChange,
        align: ci === 0 ? "left" : "center", valign: "middle", margin: 0
      });
    });
  });
}
```

### 5. 图表说明区（右侧或下方 Insight 块）

```javascript
function addChartInsight(slide, pres, theme, x, y, w, insights) {
  // insights: [{ label, text }]
  let curY = y;
  insights.forEach(item => {
    // 数据蓝小方块
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: curY + 0.06, w: 0.08, h: 0.08,
      fill: { color: theme.secondary }
    });
    slide.addText(item.label, {
      x: x + 0.16, y: curY, w: w - 0.16, h: 0.26,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    curY += 0.26;
    slide.addText(item.text, {
      x: x + 0.16, y: curY, w: w - 0.16, h: 0.32,
      fontSize: 10, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", valign: "top", margin: 0
    });
    curY += 0.38;
  });
}
```

### 6. 章节分隔页

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 数据蓝竖线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.5, y: 1.0, w: 0.08, h: 3.5,
    fill: { color: theme.secondary }
  });
  // 章节数字
  slide.addText(String(num).padStart(2, '0'), {
    x: 0.75, y: 0.8, w: 3.0, h: 1.2,
    fontSize: 80, fontFace: "Arial Black",
    color: "FFFFFF", bold: true, align: "left", margin: 0,
    transparency: 80
  });
  // 标题
  slide.addText(title, {
    x: 0.75, y: 2.1, w: 8.5, h: 0.9,
    fontSize: 32, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.75, y: 3.1, w: 7.0, h: 0.45,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 7. 图表模板

**数据分析风图表必须服务于数据可读性，颜色语义严格区分：数据蓝=正常/主系列，生长绿=正向/达成，警示橙=负向/风险。**

```javascript
// 数据分析风图表基础函数
function addDataChart(slide, pres, theme, type, chartData, opts = {}) {
  const defaults = {
    // 主系列用数据蓝，正向用生长绿，负向用警示橙，其余辅助色
    chartColors: [theme.secondary, theme.positive, theme.accent, "3B9FDE", "5EC48C"],
    chartArea: { fill: { color: theme.bg } },
    catAxisLabelColor: theme.mutedText,
    valAxisLabelColor: theme.mutedText,
    valGridLine: { color: theme.border, size: 0.5 },
    catGridLine: { style: "none" },         // 横向网格线隐藏，减少视觉干扰
    showValue: true,
    dataLabelColor: theme.bodyText,
    dataLabelFontSize: 10,
    dataLabelFontFace: "Microsoft YaHei",
    showLegend: chartData.length > 1,       // 多系列才显示图例
    legendPos: "b",
    legendFontSize: 10,
    legendFontFace: "Microsoft YaHei",
    legendColor: theme.mutedText,
  };
  slide.addChart(type, chartData, { ...defaults, ...opts });
}
```

**图表 + 右侧洞察布局（左 60% 图表 + 右 40% Insight，对比分析用）：**

```javascript
function createDataChartSlide(pres, theme, title, chartData, chartType, insights, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addDataSlideTitle(slide, pres, theme, title, source);

  // 左侧图表区（60% 宽度）
  addDataChart(slide, pres, theme, chartType, chartData, {
    x: 0.4, y: 1.0, w: 6.0, h: 4.0,
    barDir: "col",
    dataLabelPosition: "outEnd",
  });

  // 右侧天蓝细竖线分隔
  slide.addShape(pres.shapes.LINE, {
    x: 6.6, y: 1.1, w: 0, h: 3.8,
    line: { color: theme.border, width: 0.75 }
  });

  // 右侧 Insight 区（最多 4 条）
  addChartInsight(slide, pres, theme, 6.8, 1.1, 2.9, insights.slice(0, 4));

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法（柱状图 + 右侧 3 条洞察）
// createDataChartSlide(pres, theme,
//   "Q2 用户活跃度同比提升 23%，核心功能贡献超 60%",
//   [{ name: "DAU", labels: ["1月","2月","3月"], values: [120, 145, 178] }],
//   pres.charts.BAR,
//   [{ label: "整体趋势", text: "活跃用户连续 3 个月增长，增速加快。" }],
//   "数据平台·2025Q2", 3
// );
```

**全宽图表页（趋势 / 时序 / 构成分析主视觉页）：**

```javascript
function createFullDataChartSlide(pres, theme, title, chartData, chartType, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addDataSlideTitle(slide, pres, theme, title, source);

  // 全宽图表，最大化数据展示面积
  addDataChart(slide, pres, theme, chartType, chartData, {
    x: 0.4, y: 1.0, w: 9.2, h: 4.0,
    barDir: "col",
    dataLabelPosition: "outEnd",
    showLegend: chartData.length > 1,
    legendPos: "b",
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法（折线图，展示 6 个月趋势）
// createFullDataChartSlide(pres, theme,
//   "用户留存率在过去 6 个月稳步回升，30 日留存达 42%",
//   [{ name: "30日留存", labels: ["1月","2月","3月","4月","5月","6月"], values: [31,33,36,38,40,42] }],
//   pres.charts.LINE,
//   "数据平台·2025Q2", 4
// );
```

### 8. SVG 内联图形（零依赖，完全同步）

无需任何外部库。在 Node.js 生成 SVG 字符串，转 base64 嵌入幻灯片。适用于 pptxgenjs 图表库无法满足的自定义可视化。

**颜色语义（数据分析风）：**
- 数据蓝 `1A7BC4` = 主数据系列、正常状态
- 生长绿 `16A34A` = 正向变化、目标达成
- 警示橙 `E85D04` = 负向变化、风险指标

```javascript
// SVG 字符串转 base64 Data URI（Node.js 同步，零依赖）
function svgToBase64(svgStr) {
  return "image/svg+xml;base64," + Buffer.from(svgStr).toString("base64");
}
```

**迷你折线（KPI 卡内趋势走势）：**

```javascript
function makeSparkline(values, color, w = 200, h = 60) {
  // 根据数据范围自动缩放，末点加高亮圆点
  const max = Math.max(...values), min = Math.min(...values);
  const range = max - min || 1;
  const step = (w - 10) / (values.length - 1);
  const pts = values.map((v, i) => {
    const px = 5 + i * step;
    const py = 5 + ((max - v) / range) * (h - 10);
    return `${px.toFixed(1)},${py.toFixed(1)}`;
  }).join(" ");
  const lastPt = pts.split(" ").pop().split(",");
  return svgToBase64(`
    <svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
      <polyline points="${pts}" fill="none" stroke="#${color}" stroke-width="2.5" stroke-linejoin="round"/>
      <circle cx="${lastPt[0]}" cy="${lastPt[1]}" r="4" fill="#${color}"/>
    </svg>
  `);
}
// 用法
// const spark = makeSparkline([42, 55, 51, 67, 72, 80, 88], "1A7BC4");
// slide.addImage({ data: spark, x: 0.4, y: 2.5, w: 2.0, h: 0.5 });
```

**KPI 卡 + Sparkline（带趋势走势的指标卡）：**

```javascript
function addKPICardWithSparkline(slide, pres, theme, x, y, w, values, value, label, change, isPositive) {
  // 颜色语义：正向用生长绿，负向用警示橙
  const changeColor = isPositive ? theme.positive : theme.accent;
  const changeSymbol = isPositive ? "↑" : "↓";
  const sparkColor = isPositive ? theme.positive : theme.accent;

  // 卡片固定高度 2.0"（含 sparkline 区域）
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 2.0,
    fill: { color: theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 顶部数据蓝强调线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.05,
    fill: { color: theme.secondary }
  });
  // 核心数值（大字）
  slide.addText(value, {
    x: x + 0.1, y: y + 0.08, w: w - 0.2, h: 0.75,
    fontSize: 44, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 变化值（正向绿/负向橙）
  if (change) {
    slide.addText(`${changeSymbol} ${change}`, {
      x: x + 0.1, y: y + 0.86, w: w - 0.2, h: 0.28,
      fontSize: 18, fontFace: "Arial Black",
      color: changeColor, bold: true,
      align: "center", margin: 0
    });
  }
  // 指标标签
  slide.addText(label, {
    x: x + 0.1, y: y + 1.17, w: w - 0.2, h: 0.24,
    fontSize: 11, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });
  // 底部 sparkline（高 0.4"）
  if (values && values.length > 1) {
    const spark = makeSparkline(values, sparkColor, 300, 80);
    slide.addImage({
      data: spark,
      x: x + 0.08, y: y + 1.52, w: w - 0.16, h: 0.4
    });
  }
}
// 用法（正向指标）
// addKPICardWithSparkline(slide, pres, theme, 0.4, 1.1, 2.1,
//   [42, 55, 51, 67, 72, 80, 88], // sparkline 数据
//   "88%", "目标达成率", "↑ 6pp", true
// );
// 用法（负向指标）
// addKPICardWithSparkline(slide, pres, theme, 2.65, 1.1, 2.1,
//   [12, 14, 18, 15, 20, 22, 25],
//   "25%", "用户流失率", "↑ 3pp", false
// );
```

**瀑布图（收入拆解 / 成本 Bridge / 同比归因分析）：**

```javascript
function makeWaterfall(items, w = 520, h = 300) {
  // items: [{ label, value, type? }]  type:"total" 为首尾汇总条
  // 颜色硬编码：数据蓝汇总、正向浮动条、负向浮动条（与数据分析风语义对齐）
  const colors = { total: "0F2B46", positive: "1A7BC4", negative: "E85D04" };
  const n = items.length;
  const padL = 40, padB = 36, padT = 24, padR = 12;
  const chartW = w - padL - padR, chartH = h - padB - padT;
  const barW = chartW / n * 0.58, barStep = chartW / n;

  // 计算每个条的底部基准和顶部位置
  let cumulative = 0;
  const bars = items.map((item, i) => {
    const isTotal = item.type === "total" || i === 0 || i === n - 1;
    let base, top;
    if (isTotal) {
      if (i === 0) { base = 0; top = item.value; cumulative = item.value; }
      else { base = 0; top = cumulative; }
    } else {
      base = cumulative;
      top = cumulative + item.value;
      cumulative += item.value;
    }
    return { ...item, base, top, isTotal, isNeg: item.value < 0 };
  });

  const allVals = bars.flatMap(b => [b.base, b.top]);
  const minVal = Math.min(0, ...allVals), maxVal = Math.max(...allVals);
  const range = maxVal - minVal || 1;
  const toY = v => padT + ((maxVal - v) / range) * chartH;
  const zeroY = toY(0);

  const shapes = bars.map((bar, i) => {
    const bx = padL + i * barStep + (barStep - barW) / 2;
    const yTop = toY(Math.max(bar.base, bar.top));
    const yBot = toY(Math.min(bar.base, bar.top));
    const bh = Math.max(2, yBot - yTop);
    // 数据分析风颜色语义：汇总=深海蓝，正向=数据蓝，负向=警示橙
    const color = bar.isTotal ? colors.total : (bar.isNeg ? colors.negative : colors.positive);

    // 浮动条之间的虚线连接线
    const nextBar = bars[i + 1];
    const connector = nextBar && !nextBar.isTotal
      ? `<line x1="${(bx + barW).toFixed(1)}" y1="${toY(bar.top).toFixed(1)}"
               x2="${(padL + (i + 1) * barStep + (barStep - barW) / 2).toFixed(1)}" y2="${toY(bar.top).toFixed(1)}"
               stroke="#CBD5E1" stroke-width="1" stroke-dasharray="3,2"/>`
      : "";

    const labelVal = bar.isTotal ? String(bar.value) : (bar.value > 0 ? `+${bar.value}` : String(bar.value));
    const insideBar = bh >= 18;
    const labelY = insideBar ? (yTop + bh / 2 + 5).toFixed(1) : (yTop - 5).toFixed(1);
    const labelColor = insideBar ? "FFFFFF" : color;

    return `
      <rect x="${bx.toFixed(1)}" y="${yTop.toFixed(1)}" width="${barW.toFixed(1)}" height="${bh.toFixed(1)}" fill="#${color}"/>
      ${connector}
      <text x="${(bx + barW / 2).toFixed(1)}" y="${labelY}" text-anchor="middle"
        font-size="11" font-weight="bold" font-family="Arial" fill="#${labelColor}">${labelVal}</text>
      <text x="${(bx + barW / 2).toFixed(1)}" y="${(h - padB + 14).toFixed(1)}" text-anchor="middle"
        font-size="11" font-family="Microsoft YaHei,Arial" fill="#64748B">${bar.label}</text>
    `;
  });

  // 零轴基准线
  const zeroLine = `<line x1="${padL}" y1="${zeroY.toFixed(1)}" x2="${w - padR}" y2="${zeroY.toFixed(1)}"
    stroke="#CBD5E1" stroke-width="1.2"/>`;

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${zeroLine}${shapes.join("")}
  </svg>`);
}
// 用法（收入 Bridge，正向用数据蓝，负向用警示橙）
// const wf = makeWaterfall([
//   { label: "去年收入", value: 850, type: "total" },
//   { label: "新客增长", value: 120 },
//   { label: "老客续签", value: 80  },
//   { label: "客户流失", value: -60 },
//   { label: "价格调整", value: -20 },
//   { label: "今年收入", value: 970, type: "total" },
// ]);
// slide.addImage({ data: wf, x: 0.4, y: 1.0, w: 9.2, h: 3.5 });
```

**水平对比条（各维度评分 / 渠道对比 / 功能覆盖率）：**

```javascript
function makeHBarChart(items, barColor, bgColor, chartW = 400) {
  // items: [{ label, value, unit? }]
  // barColor/bgColor 不含 # 前缀
  const barH = 22, gap = 12, labelW = 90, maxBarW = chartW - labelW - 55;
  const maxVal = Math.max(...items.map(d => d.value));
  const rows = items.map((d, i) => {
    const y = i * (barH + gap) + 16;
    const bw = Math.round((d.value / maxVal) * maxBarW);
    return `
      <text x="0" y="${y + barH * 0.72}" font-size="13" font-family="Microsoft YaHei,Arial" fill="#64748B">${d.label}</text>
      <rect x="${labelW}" y="${y}" width="${maxBarW}" height="${barH}" rx="3" fill="#${bgColor}"/>
      <rect x="${labelW}" y="${y}" width="${bw}" height="${barH}" rx="3" fill="#${barColor}"/>
      <text x="${labelW + bw + 8}" y="${y + barH * 0.72}" font-size="13" font-family="Arial Black" fill="#${barColor}">${d.value}${d.unit || ""}</text>
    `;
  }).join("");
  const svgH = items.length * (barH + gap) + 20;
  return svgToBase64(`<svg width="${chartW}" height="${svgH}" xmlns="http://www.w3.org/2000/svg">${rows}</svg>`);
}
// 用法（渠道转化率对比，主系列用数据蓝）
// const hbar = makeHBarChart([
//   { label: "直接访问", value: 85, unit: "%" },
//   { label: "搜索引擎", value: 62, unit: "%" },
//   { label: "社交媒体", value: 47, unit: "%" },
//   { label: "邮件营销", value: 31, unit: "%" },
// ], "1A7BC4", "EBF4FF");
// slide.addImage({ data: hbar, x: 0.4, y: 1.1, w: 5.5, h: 2.0 });
```

**小多图 Dashboard（4 指标同时展示，2×2 布局）：**

```javascript
function makeSmallMultiples(charts, w = 860, h = 380) {
  // charts: [{ title, values, labels, color? }]，最多 4 个
  // 每格绘制简单柱状图 + 标题 + 最新值，适合 4 指标 Dashboard 页
  const cols = 2, rows = 2;
  const padInner = 20, padOuter = 16;
  const cellW = (w - padOuter * 2 - padInner * (cols - 1)) / cols;
  const cellH = (h - padOuter * 2 - padInner * (rows - 1)) / rows;

  const cells = charts.slice(0, 4).map((chart, idx) => {
    const col = idx % cols, row = Math.floor(idx / cols);
    const cx = padOuter + col * (cellW + padInner);
    const cy = padOuter + row * (cellH + padInner);
    const color = chart.color || "1A7BC4";

    // 单元格背景
    const bg = `<rect x="${cx}" y="${cy}" width="${cellW}" height="${cellH}" rx="4"
      fill="#EBF4FF" stroke="#CBD5E1" stroke-width="1"/>`;

    // 标题
    const titleEl = `<text x="${cx + cellW / 2}" y="${cy + 22}" text-anchor="middle"
      font-size="13" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="#0F2B46">${chart.title}</text>`;

    // 最新值（右上角大字）
    const latest = chart.values[chart.values.length - 1];
    const latestEl = `<text x="${cx + cellW - 12}" y="${cy + 22}" text-anchor="end"
      font-size="15" font-weight="bold" font-family="Arial Black" fill="#${color}">${latest}</text>`;

    // 迷你柱状图（底部区域）
    const barAreaY = cy + 38, barAreaH = cellH - 52;
    const barAreaW = cellW - 20;
    const vals = chart.values;
    const maxV = Math.max(...vals) || 1;
    const bw = Math.floor(barAreaW / vals.length) - 3;
    const bars = vals.map((v, i) => {
      const bh = Math.round((v / maxV) * barAreaH);
      const bx = cx + 10 + i * (bw + 3);
      const by = barAreaY + barAreaH - bh;
      const isLast = i === vals.length - 1;
      const fillColor = isLast ? color : `${color}80`;
      return `<rect x="${bx}" y="${by}" width="${bw}" height="${bh}" rx="2" fill="#${fillColor}"/>`;
    }).join("");

    // X 轴标签（仅首尾）
    const labelsArr = chart.labels || [];
    const firstLabel = labelsArr[0] || "";
    const lastLabel = labelsArr[labelsArr.length - 1] || "";
    const axisLabels = `
      <text x="${cx + 10}" y="${barAreaY + barAreaH + 14}" font-size="9"
        font-family="Arial" fill="#64748B">${firstLabel}</text>
      <text x="${cx + cellW - 10}" y="${barAreaY + barAreaH + 14}" text-anchor="end"
        font-size="9" font-family="Arial" fill="#64748B">${lastLabel}</text>
    `;

    return bg + titleEl + latestEl + bars + axisLabels;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${cells.join("")}
  </svg>`);
}
// 用法（4 指标 Dashboard）
// const sm = makeSmallMultiples([
//   { title: "DAU（万）",    values: [42,48,51,55,60,67,72], labels: ["1月","7月"] },
//   { title: "付费转化率",   values: [3.1,3.4,3.2,3.8,4.1,4.3,4.6], labels: ["1月","7月"], color: "16A34A" },
//   { title: "流失率",       values: [12,13,15,14,16,18,20], labels: ["1月","7月"], color: "E85D04" },
//   { title: "ARPU（元）",   values: [28,30,29,33,35,38,40], labels: ["1月","7月"] },
// ]);
// slide.addImage({ data: sm, x: 0.4, y: 1.0, w: 9.2, h: 4.1 });
```

## 5 种页面类型

### Cover（封面）

白色背景，标题 + 副标题（报告周期 / 数据截止日期）。右侧可放部门标识或数据看板示意色块。

```javascript
slide.background = { color: theme.bg };

slide.addText("报告标题", {
  x: 0.4, y: 1.4, w: 7.5, h: 1.2,
  fontSize: 38, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true, align: "left", margin: 0
});

// 数据蓝分隔线
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0.4, y: 2.75, w: 2.0, h: 0.04,
  fill: { color: theme.secondary }
});

slide.addText("数据截止：2025 年 Q1  ·  产品数据团队", {
  x: 0.4, y: 2.95, w: 7.0, h: 0.4,
  fontSize: 14, fontFace: "Microsoft YaHei",
  color: theme.mutedText, align: "left", margin: 0
});
```

### TOC（目录）

```javascript
function createTOCSlide(pres, theme, chapters, slideNum) {
  // chapters: [{ title, question }]，最多 6 个章节
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧窄色带（深海蓝背景，宽 2.0"）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 2.0, h: 5.625,
    fill: { color: theme.primary }
  });

  // 左侧"本次汇报"文字（竖排效果，上方）
  slide.addText("本次汇报", {
    x: 0.05, y: 1.6, w: 1.9, h: 0.5,
    fontSize: 16, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "center", valign: "middle", margin: 0
  });

  // 左侧英文标签（REPORT，下方辅助）
  slide.addText("REPORT", {
    x: 0.05, y: 2.18, w: 1.9, h: 0.35,
    fontSize: 11, fontFace: "Arial",
    color: theme.secondary, bold: false,
    align: "center", valign: "middle", margin: 0,
    transparency: 30
  });

  // 左侧数据蓝装饰竖线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 1.88, y: 0.5, w: 0.04, h: 4.625,
    fill: { color: theme.secondary }
  });

  // 右侧天蓝细竖线分隔（色带外侧）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 2.06, y: 0.5, w: 0.02, h: 4.625,
    fill: { color: theme.border }
  });

  // 右侧章节列表
  const startX = 2.3, startY = 0.52;
  const itemH = 0.78;
  chapters.slice(0, 6).forEach((ch, i) => {
    const iy = startY + i * itemH;

    // 数据蓝圆形序号
    slide.addShape(pres.shapes.OVAL, {
      x: startX, y: iy + 0.06, w: 0.32, h: 0.32,
      fill: { color: theme.secondary }
    });
    slide.addText(String(i + 1), {
      x: startX, y: iy + 0.06, w: 0.32, h: 0.32,
      fontSize: 12, fontFace: "Arial", color: "FFFFFF",
      bold: true, align: "center", valign: "middle", margin: 0
    });

    // 章节竖线（数字右侧）
    slide.addShape(pres.shapes.RECTANGLE, {
      x: startX + 0.4, y: iy + 0.1, w: 0.03, h: 0.54,
      fill: { color: theme.border }
    });

    // 章节标题（粗体，深海蓝）
    slide.addText(ch.title, {
      x: startX + 0.52, y: iy + 0.04, w: 7.1, h: 0.3,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });

    // 核心问题说明（正常，板岩灰）
    if (ch.question) {
      slide.addText(ch.question, {
        x: startX + 0.52, y: iy + 0.36, w: 7.1, h: 0.28,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.mutedText,
        align: "left", valign: "middle", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
// createTOCSlide(pres, theme, [
//   { title: "整体指标概览",   question: "本季度核心 KPI 达成情况如何？" },
//   { title: "用户增长分析",   question: "新增用户来自哪些渠道？增速是否健康？" },
//   { title: "留存与活跃趋势", question: "用户行为出现了哪些值得关注的变化？" },
//   { title: "收入拆解归因",   question: "收入增长的主要驱动因素是什么？" },
//   { title: "风险与异常",     question: "有哪些指标出现了预警信号？" },
//   { title: "结论与建议",     question: "下一步应优先采取哪些行动？" },
// ], 2);
```

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，深海蓝背景 + 数据蓝竖线装饰。

### Content（内容页）

背景 `theme.bg`，标题用 `addDataSlideTitle`（必须是结论句），页码用 `addPageBadge`。

| 内容关系 | 布局 / 函数 |
|----------|------------|
| 核心 KPI 进展 | 横排 3–5 个 `addKPIChangeCard` |
| 图表 + 分析 | 左 70% 图表占位 + 右 30% `addChartInsight` |
| 对比数据 | 左右两栏，用 `positive`/`accent` 区分好坏 |
| 数据明细 | `addDataTable`，≤ 8 行，超出拆页 |
| 趋势说明 | 横向时间线 + 关键事件标注 |
| 趋势 / 时序分析 | `createFullDataChartSlide`（LINE） |
| 对比 + 洞察 | `createDataChartSlide`（BAR + 右侧 Insight） |
| 构成 / 占比 | `createFullDataChartSlide`（PIE/DOUGHNUT） |
| 收入拆解 / 归因分析 | `makeWaterfall` SVG |
| KPI 含趋势走势 | `addKPICardWithSparkline` |
| 4 指标 Dashboard | `makeSmallMultiples` SVG |
| 各维度对比 | `makeHBarChart` SVG |

### Summary（总结页）

```javascript
function createDataSummarySlide(pres, theme, findings, action, source, slideNum) {
  // findings: [{ label, text }]，最多 5 条核心发现
  // action: 建议行动项文字（字符串）
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 标题栏（深海蓝，全宽，高 0.75"）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.75,
    fill: { color: theme.primary }
  });
  // 白色"核心发现"文字
  slide.addText("核心发现", {
    x: 0.4, y: 0, w: 5.0, h: 0.75,
    fontSize: 20, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 标题栏右侧英文辅助标签
  slide.addText("KEY FINDINGS", {
    x: 5.4, y: 0, w: 4.2, h: 0.75,
    fontSize: 11, fontFace: "Arial",
    color: theme.secondary, bold: false,
    align: "right", valign: "middle", margin: 0,
    transparency: 25
  });

  // 内容区：用 addChartInsight 格式列出核心发现（最多 5 条）
  addChartInsight(slide, pres, theme, 0.4, 0.88, 9.2, findings.slice(0, 5));

  // 底部数据蓝全宽分隔线
  const actionY = 4.58;
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: actionY, w: 10, h: 0.03,
    fill: { color: theme.secondary }
  });

  // "建议行动"标签（数据蓝小标签块）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.4, y: actionY + 0.1, w: 0.8, h: 0.24,
    fill: { color: theme.secondary }
  });
  slide.addText("建议行动", {
    x: 0.4, y: actionY + 0.1, w: 0.8, h: 0.24,
    fontSize: 9, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "center", valign: "middle", margin: 0
  });

  // 建议行动文字（加粗数据蓝）
  if (action) {
    slide.addText(action, {
      x: 1.32, y: actionY + 0.08, w: 7.9, h: 0.3,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.secondary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
  }

  // 来源注释（左下角，mutedText）
  if (source) {
    slide.addText(`数据来源：${source}`, {
      x: 0.4, y: 5.32, w: 6.0, h: 0.22,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
// createDataSummarySlide(pres, theme,
//   [
//     { label: "用户规模",   text: "DAU 突破 150 万，同比增长 31%，增速连续 3 个季度加快。" },
//     { label: "付费转化",   text: "付费率达 4.6%，较去年提升 1.5pp，高于行业均值 3.2%。" },
//     { label: "留存风险",   text: "30 日留存率连续 2 个月下滑，需重点关注流失路径。" },
//     { label: "收入驱动",   text: "新客增长贡献 62% 的收入增量，老客 ARPU 同比持平。" },
//   ],
//   "优先修复 D3–D7 留存漏斗，同步启动高价值用户激励计划（目标：Q3 末 30 日留存回升至 40%）。",
//   "数据平台·2025Q2",
//   12
// );
```

## 视觉选择决策树

> **强制规则：每张内容页必须包含图表或数据可视化元素，禁止纯文字分析页。**

| 内容类型 | 推荐组件 | 颜色语义提示 |
|----------|----------|-------------|
| 单指标趋势（时间轴） | `createFullDataChartSlide`（LINE） | 主系列用 `secondary`（数据蓝） |
| 多指标趋势对比 | `createFullDataChartSlide`（LINE，多系列） | 正向系列用 `positive`，负向用 `accent` |
| 柱状对比 + 文字洞察 | `createDataChartSlide`（BAR） | 差异列用 `accent` 标注 |
| 构成 / 占比分析 | `createFullDataChartSlide`（PIE 或 DOUGHNUT） | 主占比 `secondary`，警示项 `accent` |
| 核心 KPI 汇总 | 横排 `addKPIChangeCard`（3–5 个） | 正向 `positive`，负向 `accent` |
| KPI + 走势趋势 | `addKPICardWithSparkline` | 正向 sparkline 绿，负向橙 |
| 4 指标 Dashboard | `makeSmallMultiples` SVG | 各指标可指定独立颜色 |
| 收入/成本 Bridge | `makeWaterfall` SVG（颜色已内置） | 汇总深海蓝，增 `1A7BC4`，减 `E85D04` |
| 维度/渠道对比 | `makeHBarChart` SVG | 主系列 `secondary`，背景 `light` |
| 数据明细表格 | `addDataTable` | 斑马行 `light`，变化值自动着色 |
| 目录页 | `createTOCSlide` | 左侧深海蓝色带，序号 `secondary` |
| 总结/结论页 | `createDataSummarySlide` | 标题栏 `primary`，行动项 `secondary` |
| 章节分隔 | `createSectionDividerSlide` | 深海蓝背景，数据蓝竖线 |

**禁止模式（严格执行）：**
- 禁止在内容页只放文字段落（必须配图表或 SVG 可视化）
- 禁止将 `accent`（警示橙）用于正常状态或纯装饰
- 禁止将 `positive`（生长绿）用于负向或下降数据
- 禁止在一页放超过 2 个独立图表（`makeSmallMultiples` 的 4 格算 1 个）
- 禁止图表无标题、无数据来源

## 数据分析风专项规则

**数据规则：**
- 所有图表必须注明数据来源和截止日期（`addDataSlideTitle` 的 `source` 参数）
- 变化值必须标明方向（`↑` / `↓`）和对比基准（环比 / 同比 / 目标值）
- 百分比变化和绝对值变化都要展示（"提升 15%（+3.2 万次）"）

**视觉规则：**
- 数据蓝（`secondary`）用于主数据系列和正常状态
- 警示橙（`accent`）专用于负向变化和风险指标，不做装饰用途
- 生长绿（`positive`）专用于达成目标和正向变化
- 每页最多使用以上三色各一次，避免彩虹图表
- 表格必须有斑马行，超过 5 列的表格必须缩减或拆分
