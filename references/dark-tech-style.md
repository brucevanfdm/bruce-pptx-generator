# Style Preset: Dark Tech（暗黑科技）

适合场景：产品发布、技术演讲、AI 能力展示、发布会风格汇报。面向科技感强、追求视觉冲击力的场合。

## 氛围

**创新进取** — 深色背景、高对比强调色、科技感图形语言。让观众感受到产品的前沿性和技术底气。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 纯白 | `FFFFFF` | 标题、主要文字 |
| `secondary` | 青绿 | `00C9A7` | 强调元素、数字、标签、按钮、图标色 |
| `accent` | 电光蓝 | `4FC3F7` | 标题下方细线、次级强调色 |
| `light` | 深灰卡片 | `1E2A3A` | 卡片背景、内容块填充 |
| `bg` | 深海蓝黑 | `0D1B2A` | 所有内容页背景 |
| `dividerBg` | 极深蓝 | `091523` | 章节分隔页背景 |
| `bodyText` | 浅灰白 | `C8D6E5` | 正文段落 |
| `mutedText` | 中灰蓝 | `7A95B0` | 次级文字、说明、描述 |
| `watermark` | 深青 | `004D40` | 章节分隔页水印数字 |
| `border` | 深蓝灰 | `1E3A4F` | 卡片边框、分隔线 |

```javascript
const theme = {
  primary:   "FFFFFF",
  secondary: "00C9A7",
  accent:    "4FC3F7",
  light:     "1E2A3A",
  bg:        "0D1B2A",
  dividerBg: "091523",
  bodyText:  "C8D6E5",
  mutedText: "7A95B0",
  watermark: "004D40",
  border:    "1E3A4F",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 40–48 | Bold | `primary`（白色） |
| 封面副标题 | Microsoft YaHei | 18–20 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 28–30 | Bold | `primary`（白色） |
| 二级标题 / 卡片标题 | Microsoft YaHei | 16–18 | Bold | `primary` |
| 三级标题 / 特性标题 | Microsoft YaHei | 14–16 | Bold | `secondary` |
| 正文 | Microsoft YaHei | 13–14 | Regular | `bodyText` |
| 说明 / 描述 | Microsoft YaHei | 11–12 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 48–64 | Bold | `secondary` 或 `accent` |
| TOC 大数字 | Arial Black | 42 | Bold | `secondary` |
| 章节分隔水印数字 | Arial Black | 200 | Bold | `watermark` |
| 标签文字 | Microsoft YaHei | 22–24 | Bold | `bg`（深色背景上的深色文字） |

## 布局网格系统

幻灯片尺寸 10" × 5.625"。与企业科技蓝相同的安全边界。

**安全边界：**

```
左边界:   x ≥ 0.45"
右边界:   x + w ≤ 9.55"
上边界:   y ≥ 1.05"
下边界:   y + h ≤ 5.0"
内容区高度: 3.95"
内容区宽度: 9.1"
```

**内容密度指引（产品发布型 — 精装标准）：**

> 本风格定位为**产品发布 / 演讲辅助型**，每张幻灯片一个核心观点，视觉冲击优先，信息量适度留白但必须有数据支撑。

- 每张内容页：核心条目 **3–5 条**，每条需 tagline（结论导向）+ 数据支撑
- **KPI 页：2–4 个核心数字，大字号 + 单位 + 变化率标签 + 底部洞察说明**
- 纯视觉叙事页：允许只有标题 + 大图形元素，但需在图形旁配合洞察标签
- **每张内容页至少包含 1 种非文字视觉**（图表 / 进度环 / 架构图 / 图标卡 / 流程图）
- 避免文字墙，优先用卡片 / 图表代替段落

## 标志性设计元素

### 1. 标题 + 青绿下划线（所有非封面页必用）

本风格标志性元素：白色标题 + 细短青绿横线，右侧延伸深蓝灰细线。

```javascript
function addSlideTitleWithAccent(slide, pres, theme, title) {
  slide.addText(title, {
    x: 0.45, y: 0.22, w: 9.1, h: 0.52,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 青绿短横线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.80, w: 0.4, h: 0.06,
    fill: { color: theme.secondary }
  });
  // 右侧延伸细线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.95, y: 0.82, w: 8.6, h: 0.01,
    fill: { color: theme.border }
  });
}
```



### 1.5 精装能力卡片（Rich Card）—— 推荐默认使用

**优先使用此组件替代基础的 `addFeatureItem`**。精装卡片包含：顶部强调色条、编号圆形、标题、tagline、带前缀的 bullet 功能列表、底部洞察说明区。

```javascript
function addDarkRichCard(slide, pres, theme, x, y, w, h, num, title, tagline, features, detail, highlight) {
  const accentColor = highlight ? theme.accent : theme.secondary;
  const bgColor = highlight ? theme.light : theme.bg; // light="1E2A3A"(深灰卡片), bg="0D1B2A"(深海底)

  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h, fill: { color: bgColor }, line: { color: theme.border, width: 0.5 } });
  // 顶部强调色条
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h: 0.07, fill: { color: accentColor } });

  // 编号圆形
  slide.addShape(pres.shapes.OVAL, { x: x + 0.18, y: y + 0.2, w: 0.46, h: 0.46, fill: { color: accentColor } });
  slide.addText(String(num), { x: x + 0.18, y: y + 0.2, w: 0.46, h: 0.46, fontSize: 14, fontFace: "Arial Black", color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0 });

  // 标题
  slide.addText(title, { x: x + 0.74, y: y + 0.16, w: w - 0.9, h: 0.34, fontSize: 13, fontFace: "Microsoft YaHei", color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0 });

  // Tagline
  slide.addText(tagline, { x: x + 0.74, y: y + 0.5, w: w - 0.9, h: 0.26, fontSize: 9.5, fontFace: "Microsoft YaHei", color: accentColor, align: "left", valign: "middle", margin: 0 });

  // 分隔线
  slide.addShape(pres.shapes.LINE, { x: x + 0.15, y: y + 0.84, w: w - 0.3, h: 0, line: { color: theme.border, width: 0.5 } });

  // Bullet 功能列表（带小方块前缀）
  const featStartY = y + 0.94;
  const featH = 0.4;
  features.forEach((f, i) => {
    const fy = featStartY + i * featH;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.18, y: fy + 0.13, w: 0.1, h: 0.1, fill: { color: accentColor } });
    slide.addText(f, { x: x + 0.34, y: fy + 0.06, w: w - 0.5, h: featH - 0.12, fontSize: 9.5, fontFace: "Microsoft YaHei", color: theme.bodyText, align: "left", valign: "middle", margin: 0 });
  });

  // 底部洞察说明区
  if (detail) {
    const footerY = y + h - 0.55;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.15, y: footerY, w: w - 0.3, h: 0.45, fill: { color: theme.bg }, line: { color: theme.border, width: 0.3 } }); // 深色背景，勿用FFFFFF
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.15, y: footerY, w: 0.05, h: 0.45, fill: { color: theme.secondary } });
    slide.addText(detail, { x: x + 0.26, y: footerY, w: w - 0.46, h: 0.45, fontSize: 8.5, fontFace: "Microsoft YaHei", color: theme.mutedText, align: "left", valign: "middle", margin: 0 });
  }
}
```

### 2. 页码徽章（所有非封面页必用）

```javascript
function addPageBadge(slide, pres, theme, num) {
  slide.addShape(pres.shapes.OVAL, {
    x: 9.3, y: 5.1, w: 0.4, h: 0.4,
    fill: { color: theme.secondary }
  });
  slide.addText(String(num), {
    x: 9.3, y: 5.1, w: 0.4, h: 0.4,
    fontSize: 12, fontFace: "Arial", color: theme.bg,
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. 章节分隔页：水印大数字 + 胶囊标签

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 超大水印数字
  slide.addText(String(num).padStart(2, '0'), {
    x: 0, y: 0.2, w: 6.5, h: 5.2,
    fontSize: 200, fontFace: "Arial Black",
    color: theme.watermark, bold: true, align: "left", margin: 0
  });

  // 胶囊标签（青绿填充）
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fill: { color: theme.secondary },
    rectRadius: 0.34
  });
  slide.addText(title, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fontSize: 22, fontFace: "Microsoft YaHei",
    color: theme.bg, bold: true, align: "center", valign: "middle", margin: 0
  });

  // 副标题
  slide.addText(subtitle, {
    x: 3.0, y: 2.78, w: 4.2, h: 0.38,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 4. 目录条目（TOC Item）

```javascript
function addTOCItem(slide, pres, theme, x, y, num, title, subtitle, maxW) {
  const numW  = 1.1;
  const numH  = 0.72;
  const divX  = x + numW + 0.05;
  const textX = divX + 0.12;
  const textW = (maxW !== undefined) ? (x + maxW - textX) : (9.55 - textX);

  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: numW, h: numH,
    fontSize: 42, fontFace: "Arial Black",
    color: theme.secondary, bold: true, align: "center", valign: "middle", margin: 0
  });
  slide.addShape(pres.shapes.RECTANGLE, {
    x: divX, y: y + 0.11, w: 0.04, h: numH - 0.22,
    fill: { color: theme.secondary }
  });
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.40,
    fontSize: 17, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "bottom", margin: 0
  });
  slide.addText(subtitle, {
    x: textX, y: y + 0.40, w: textW, h: 0.30,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", valign: "top", margin: 0
  });
}
```

### 5. 特性条目（Feature Item）

```javascript
function addFeatureItem(slide, pres, theme, x, y, num, title, description, zoneW) {
  const circleSize = 0.44;
  const gap = 0.14;
  const textX = x + circleSize + gap;
  const textW = zoneW - circleSize - gap;

  slide.addShape(pres.shapes.OVAL, {
    x: x, y: y + 0.01, w: circleSize, h: circleSize,
    fill: { color: theme.secondary }
  });
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y + 0.01, w: circleSize, h: circleSize,
    fontSize: 13, fontFace: "Arial", color: theme.bg,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.32,
    fontSize: 15, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  slide.addText(description, {
    x: textX, y: y + 0.34, w: textW, h: 0.72,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", valign: "top", margin: 0
  });
}
```

### 6. KPI 指标卡（深色卡片版）

```javascript
function addKPICard(slide, pres, theme, x, y, w, h, value, unit, label, color) {
  // 深色卡片背景 + 左侧竖向强调色条（替代顶部细条，更有科技感）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: h,
    fill: { color: theme.light },
    line: { color: theme.border, width: 1 }
  });
  // 左侧强调色竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: 0.06, h: h,
    fill: { color: color || theme.secondary }
  });
  // 大数字
  slide.addText(value, {
    x: x, y: y + 0.2, w: w, h: 1.0,
    fontSize: 56, fontFace: "Arial Black",
    color: color || theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  if (unit) {
    slide.addText(unit, {
      x: x, y: y + 0.9, w: w, h: 0.38,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: color || theme.secondary, bold: true,
      align: "center", margin: 0
    });
  }
  slide.addText(label, {
    x: x + 0.1, y: y + h - 0.42, w: w - 0.2, h: 0.38,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });
}
```

### 7. 图表（暗色主题）

**深色背景图表的关键：`chartArea` 必须用深色背景，轴标签必须用浅色，否则文字在深背景上不可见。**

```javascript
// 暗黑科技风格基础图表函数
function addDarkChart(slide, pres, theme, type, chartData, opts = {}) {
  // chartArea 必须用深色背景，否则图表区域会显示白色
  const defaults = {
    chartColors: ["00C9A7", "4FC3F7", "67E8F9", "A7F3D0"],
    chartArea: { fill: { color: theme.bg } },      // 深色背景，关键！
    catAxisLabelColor: theme.bodyText,              // 浅色轴标签，在深背景下可见
    valAxisLabelColor: theme.bodyText,
    valGridLine: { color: theme.border, size: 0.5 }, // 深色网格线
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

**图表 + 右侧洞察布局（左图右文）：**

```javascript
function createDarkChartSlide(pres, theme, title, chartData, chartType, insights, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };         // 深色背景
  addSlideTitleWithAccent(slide, pres, theme, title);

  // 左侧图表区（深色 chartArea 背景在 addDarkChart 内已设置）
  addDarkChart(slide, pres, theme, chartType, chartData, {
    x: 0.45, y: 1.05, w: 5.8, h: 3.8,
    barDir: "col",
    dataLabelPosition: "outEnd",
  });

  // 右侧深色分隔线
  slide.addShape(pres.shapes.LINE, {
    x: 6.4, y: 1.15, w: 0, h: 3.6,
    line: { color: theme.border, width: 0.75 }
  });

  // 右侧洞察要点（最多 3 条）
  insights.slice(0, 3).forEach((item, i) => {
    const iy = 1.2 + i * 1.22;
    // 青绿色方块序号
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 6.5, y: iy, w: 0.30, h: 0.30,
      fill: { color: theme.secondary }
    });
    slide.addText(String(i + 1), {
      x: 6.5, y: iy, w: 0.30, h: 0.30,
      fontSize: 11, fontFace: "Arial", color: theme.bg,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    // 白色洞察标题
    slide.addText(item.title, {
      x: 6.92, y: iy, w: 2.6, h: 0.30,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    // 灰色说明文字
    if (item.desc) {
      slide.addText(item.desc, {
        x: 6.92, y: iy + 0.33, w: 2.6, h: 0.65,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.mutedText, align: "left", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
createDarkChartSlide(pres, theme, "AI 能力平台三项核心指标持续提升",
  [{ name: "准确率", labels: ["Q1","Q2","Q3","Q4"], values: [72,78,84,91] }],
  pres.charts.LINE,
  [
    { title: "准确率突破 90%", desc: "Q4 模型迭代后推理准确率达 91%，超出目标 6ppt" },
    { title: "延迟降低 40%", desc: "边缘部署优化后 P99 延迟从 180ms 降至 108ms" },
    { title: "成本下降 35%", desc: "混合云架构切换后单次推理算力成本持续优化" },
  ],
  5
);
```

**全宽图表页（主视觉数据页）：**

```javascript
function createFullDarkChartSlide(pres, theme, title, chartData, chartType, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };         // 深色背景
  addSlideTitleWithAccent(slide, pres, theme, title);

  // 全宽图表，chartArea 深色由 addDarkChart 保证
  addDarkChart(slide, pres, theme, chartType, chartData, {
    x: 0.45, y: 1.05, w: 9.1, h: 3.9,
    barDir: "col",
    dataLabelPosition: "outEnd",
    showLegend: chartData.length > 1,
    legendPos: "b",
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
createFullDarkChartSlide(pres, theme, "平台月活用户连续 8 个月超预期增长",
  [
    { name: "实际值", labels: ["1月","2月","3月","4月","5月","6月","7月","8月"], values: [12,18,24,31,40,52,65,80] },
    { name: "目标值", labels: ["1月","2月","3月","4月","5月","6月","7月","8月"], values: [10,15,20,28,36,45,55,68] },
  ],
  pres.charts.LINE,
  6
);
```

### 8. SVG 内联图形（零依赖，完全同步）

无需任何外部库。在 Node.js 生成 SVG 字符串，转 base64 嵌入幻灯片。深色背景下文字必须用浅色（白色或 `C8D6E5`）。

```javascript
// SVG 转 base64 工具函数
function svgToBase64(svgStr) {
  return "image/svg+xml;base64," + Buffer.from(svgStr).toString("base64");
}
```

**进度环（完成率 / 目标达成 / 能力覆盖率）：**

```javascript
function makeProgressRing(percent, fgColor, bgColor, label = "完成率", size = 200) {
  // 背景透明，让幻灯片深色背景透出；文字用浅灰白，在深背景下可见
  const r = 76, cx = size / 2, cy = size / 2;
  const circ = 2 * Math.PI * r;
  const dash = (circ * percent / 100).toFixed(1);
  return svgToBase64(`
    <svg width="${size}" height="${size}" xmlns="http://www.w3.org/2000/svg">
      <circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="#${bgColor}" stroke-width="14"/>
      <circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="#${fgColor}" stroke-width="14"
        stroke-dasharray="${dash} ${circ.toFixed(1)}" stroke-linecap="round"
        transform="rotate(-90 ${cx} ${cy})"/>
      <text x="${cx}" y="${cy - 8}" text-anchor="middle"
        font-size="40" font-weight="bold" font-family="Arial" fill="#${fgColor}">${percent}%</text>
      <text x="${cx}" y="${cy + 22}" text-anchor="middle"
        font-size="16" font-family="Microsoft YaHei,Arial" fill="#C8D6E5">${label}</text>
    </svg>
  `);
}
// 用法
const ring = makeProgressRing(78, "00C9A7", "1E3A4F", "完成率");
slide.addImage({ data: ring, x: 1.0, y: 1.5, w: 1.5, h: 1.5 });
```

**趋势迷你折线（KPI 卡内小型走势图）：**

```javascript
function makeSparkline(values, color, w = 200, h = 60) {
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
// 用法（KPI 卡底部趋势线，颜色传入青绿或电光蓝）
const spark = makeSparkline([42, 55, 51, 67, 72, 80, 88], "00C9A7");
slide.addImage({ data: spark, x: 0.6, y: 2.2, w: 2.0, h: 0.5 });
```

**横向时间轴（技术路线图 / 里程碑规划）：**

```javascript
function makeDarkTimeline(milestones, w = 860, h = 160) {
  // milestones: [{ date, title, desc?, done?, current? }]
  // done: 已完成（青绿实心）current: 当前（电光蓝 + 发光环）future: 未来（空心白色）
  const n = milestones.length;
  const padH = 50, lineY = h * 0.48;
  const step = (w - padH * 2) / Math.max(n - 1, 1);
  const currIdx = milestones.findIndex(m => m.current);

  // 背景线：深蓝灰色
  const bgLine = `<line x1="${padH}" y1="${lineY}" x2="${w - padH}" y2="${lineY}"
    stroke="#1E3A4F" stroke-width="2.5"/>`;
  // 进度线：青绿色（已完成部分）
  const progressLine = currIdx > 0
    ? `<line x1="${padH}" y1="${lineY}" x2="${(padH + currIdx * step).toFixed(1)}" y2="${lineY}"
        stroke="#00C9A7" stroke-width="2.5"/>`
    : "";

  const nodes = milestones.map((m, i) => {
    const x = padH + i * step;
    const isDone = m.done || (currIdx >= 0 && i < currIdx);
    const isCurrent = m.current;
    const r = isCurrent ? 10 : 7;
    // 已完成：青绿实心；当前：电光蓝实心；未来：空心白色
    const fill = isDone ? "00C9A7" : (isCurrent ? "4FC3F7" : "none");
    const stroke = isDone ? "00C9A7" : (isCurrent ? "4FC3F7" : "FFFFFF");
    const sw = isCurrent ? 3 : 2;
    // 当前节点发光环效果（两层半透明圆）
    const ring = isCurrent ? `
      <circle cx="${x.toFixed(1)}" cy="${lineY}" r="20"
        fill="none" stroke="#4FC3F7" stroke-width="1" opacity="0.25"/>
      <circle cx="${x.toFixed(1)}" cy="${lineY}" r="14"
        fill="none" stroke="#4FC3F7" stroke-width="1.5" opacity="0.45"/>
    ` : "";
    // 日期标签：浅灰白
    // 标题标签：已完成用白色，当前用电光蓝，未来用中灰蓝
    const titleFill = isCurrent ? "4FC3F7" : (isDone ? "C8D6E5" : "7A95B0");
    return `
      ${ring}
      <circle cx="${x.toFixed(1)}" cy="${lineY}" r="${r}" fill="#${fill}" stroke="#${stroke}" stroke-width="${sw}"/>
      <text x="${x.toFixed(1)}" y="${(lineY - r - 7).toFixed(1)}" text-anchor="middle"
        font-size="10" font-family="Arial" fill="#7A95B0">${m.date}</text>
      <text x="${x.toFixed(1)}" y="${(lineY + r + 16).toFixed(1)}" text-anchor="middle"
        font-size="12" font-weight="${isCurrent ? "bold" : "normal"}"
        font-family="Microsoft YaHei,Arial" fill="#${titleFill}">${m.title}</text>
      ${m.desc ? `<text x="${x.toFixed(1)}" y="${(lineY + r + 30).toFixed(1)}" text-anchor="middle"
        font-size="10" font-family="Microsoft YaHei,Arial" fill="#7A95B0">${m.desc}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${bgLine}${progressLine}${nodes.join("")}
  </svg>`);
}
// 用法（技术路线图，铺满幻灯片底部）
const timeline = makeDarkTimeline([
  { date: "Q1 2024", title: "基础架构", done: true },
  { date: "Q2 2024", title: "模型训练", done: true },
  { date: "Q3 2024", title: "平台上线", current: true, desc: "进行中" },
  { date: "Q4 2024", title: "生态接入" },
  { date: "Q1 2025", title: "规模扩张" },
]);
slide.addImage({ data: timeline, x: 0.45, y: 3.2, w: 9.1, h: 1.6 });
```

**科技感金字塔（技术架构层级 / 能力模型）：**

```javascript
function makeDarkPyramid(layers, w = 500, h = 360) {
  // layers: [{ label, value? }]，顺序从顶到底（顶层最窄）
  // 颜色从顶到底：极深 → 次深，层间分隔线用青绿色
  const colors = ["091523", "0D1B2A", "1E2A3A", "1E3A4F"];
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
    // 层间青绿分隔线（顶部边界）
    const divLine = i > 0
      ? `<line x1="${(cx - wTop / 2).toFixed(1)}" y1="${y}"
               x2="${(cx + wTop / 2).toFixed(1)}" y2="${y}"
               stroke="#00C9A7" stroke-width="1.5"/>`
      : "";
    return `
      <polygon points="${pts}" fill="#${color}"/>
      ${divLine}
      <text x="${cx}" y="${(textY + fs * 0.35).toFixed(1)}" text-anchor="middle"
        font-size="${fs}" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="#FFFFFF">${layer.label}</text>
      ${layer.value ? `<text x="${cx}" y="${(textY + fs * 1.2).toFixed(1)}" text-anchor="middle"
        font-size="${Math.round(fs * 0.78)}" font-family="Arial" fill="#C8D6E5">${layer.value}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">${shapes.join("")}</svg>`);
}
// 用法（4 层技术架构）
const pyramid = makeDarkPyramid([
  { label: "业务应用层" },
  { label: "AI 能力层",   value: "推理 · 训练 · 微调" },
  { label: "数据平台层",  value: "湖仓一体 · 实时流" },
  { label: "基础设施层",  value: "GPU 集群 · 边缘节点" },
]);
slide.addImage({ data: pyramid, x: 0.5, y: 1.1, w: 4.8, h: 3.5 });
```

**深色漏斗（转化分析 / 技术管道 / 业务阶段）：**

```javascript
function makeDarkFunnel(stages, w = 400, h = 320) {
  // stages: [{ label, value, rate? }]，顺序从上到下（顶层最宽）
  // 深色阶梯颜色数组，顶部强调条用青绿
  const colors = ["0D1B2A", "1E2A3A", "1E3A4F", "263547"];
  const n = stages.length;
  const topW = w * 0.90, botW = w * 0.22;
  const cx = w / 2, stageH = h / n, gap = 3;

  const shapes = stages.map((stage, i) => {
    const wTop = topW + (botW - topW) * (i / n);
    const wBot = topW + (botW - topW) * ((i + 1) / n);
    const y = i * stageH;
    const pts = [
      `${(cx - wTop / 2 + gap).toFixed(1)},${y}`,
      `${(cx + wTop / 2 - gap).toFixed(1)},${y}`,
      `${(cx + wBot / 2 - gap).toFixed(1)},${(y + stageH - gap).toFixed(1)}`,
      `${(cx - wBot / 2 + gap).toFixed(1)},${(y + stageH - gap).toFixed(1)}`,
    ].join(" ");
    const color = colors[i % colors.length];
    const textY = y + stageH / 2;
    const fs = Math.min(14, Math.round(stageH * 0.30));
    const rateX = (cx + wTop / 2 + 8).toFixed(1);
    // 顶部青绿强调条
    const topAccent = i === 0
      ? `<line x1="${(cx - wTop / 2 + gap).toFixed(1)}" y1="${y}"
               x2="${(cx + wTop / 2 - gap).toFixed(1)}" y2="${y}"
               stroke="#00C9A7" stroke-width="3"/>`
      : "";
    return `
      <polygon points="${pts}" fill="#${color}"/>
      ${topAccent}
      <text x="${cx}" y="${(textY - fs * 0.3).toFixed(1)}" text-anchor="middle"
        font-size="${fs}" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="#FFFFFF">${stage.label}</text>
      <text x="${cx}" y="${(textY + fs * 0.9).toFixed(1)}" text-anchor="middle"
        font-size="${Math.round(fs * 0.88)}" font-family="Arial Black" fill="#00C9A7">${stage.value}</text>
      ${stage.rate ? `<text x="${rateX}" y="${(textY + 4).toFixed(1)}" font-size="11" font-family="Arial" fill="#7A95B0">${stage.rate}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">${shapes.join("")}</svg>`);
}
// 用法（4 阶段技术管道）
const funnel = makeDarkFunnel([
  { label: "潜在用户",  value: "120,000", rate: "100%" },
  { label: "注册激活",  value: "48,000",  rate: "40%" },
  { label: "深度使用",  value: "15,600",  rate: "13%" },
  { label: "付费转化",  value: "4,200",   rate: "3.5%" },
]);
slide.addImage({ data: funnel, x: 0.5, y: 1.1, w: 4.0, h: 3.5 });
```

**深色 2×2 矩阵（产品定位 / 竞争分析 / 优先级矩阵）：**

```javascript
function makeDark2x2Matrix(quadrants, xAxis, yAxis, w = 440, h = 380) {
  // quadrants: [TL, TR, BL, BR]，每项 { label, sublabel, highlight? }
  // xAxis: { left, right }，yAxis: { top, bottom }
  // highlight: true 时该象限用青绿高亮（文字用深色）
  const pad = 44, qw = (w - pad * 2) / 2, qh = (h - pad * 2) / 2;
  const positions = [
    { row: 0, col: 0 }, { row: 0, col: 1 },
    { row: 1, col: 0 }, { row: 1, col: 1 },
  ];

  const quads = quadrants.map((q, i) => {
    const { row, col } = positions[i];
    const x = pad + col * qw, y = pad + row * qh;
    // 高亮象限用青绿，普通象限用深灰卡片色
    const bg = q.highlight ? "00C9A7" : "1E2A3A";
    // 高亮象限文字用深色，普通象限文字用白色
    const textColor = q.highlight ? "0D1B2A" : "FFFFFF";
    const subColor  = q.highlight ? "091523" : "7A95B0";
    return `
      <rect x="${x}" y="${y}" width="${qw}" height="${qh}" fill="#${bg}" stroke="#1E3A4F" stroke-width="1.5"/>
      <text x="${(x + qw / 2).toFixed(1)}" y="${(y + qh / 2 - 8).toFixed(1)}" text-anchor="middle"
        font-size="15" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="#${textColor}">${q.label}</text>
      ${q.sublabel ? `<text x="${(x + qw / 2).toFixed(1)}" y="${(y + qh / 2 + 14).toFixed(1)}" text-anchor="middle"
        font-size="11" font-family="Microsoft YaHei,Arial" fill="#${subColor}">${q.sublabel}</text>` : ""}
    `;
  });

  // 电光蓝坐标轴（带箭头）
  const ax = pad, ay = pad + qh, aex = pad + qw * 2, aey = pad;
  const axes = `
    <defs>
      <marker id="arh" markerWidth="7" markerHeight="7" refX="5" refY="3.5" orient="auto">
        <polygon points="0,0 7,3.5 0,7" fill="#4FC3F7"/>
      </marker>
    </defs>
    <line x1="${ax}" y1="${ay}" x2="${aex + 16}" y2="${ay}"
      stroke="#4FC3F7" stroke-width="1.5" marker-end="url(#arh)"/>
    <line x1="${pad + qw}" y1="${pad + qh * 2}" x2="${pad + qw}" y2="${aey - 16}"
      stroke="#4FC3F7" stroke-width="1.5" marker-end="url(#arh)"/>
  `;

  // 轴标签：电光蓝高亮端，中灰蓝低侧
  const labels = `
    <text x="${aex + 20}" y="${ay + 4}" font-size="11" font-family="Arial" fill="#4FC3F7">${xAxis?.right || ""}</text>
    <text x="${ax - 4}" y="${ay + 4}" text-anchor="end" font-size="11" font-family="Arial" fill="#7A95B0">${xAxis?.left || ""}</text>
    <text x="${pad + qw}" y="${aey - 20}" text-anchor="middle" font-size="11" font-family="Arial" fill="#4FC3F7">${yAxis?.top || ""}</text>
    <text x="${pad + qw}" y="${pad + qh * 2 + 16}" text-anchor="middle" font-size="11" font-family="Arial" fill="#7A95B0">${yAxis?.bottom || ""}</text>
  `;

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${axes}${quads.join("")}${labels}
  </svg>`);
}
// 用法（产品竞争定位矩阵）
const matrix = makeDark2x2Matrix(
  [
    { label: "观察区",   sublabel: "高技术·低市场" },
    { label: "核心优势", sublabel: "高技术·高市场", highlight: true },
    { label: "淘汰区",   sublabel: "低技术·低市场" },
    { label: "机会区",   sublabel: "低技术·高市场" },
  ],
  { left: "低市场吸引力", right: "高市场吸引力" },
  { top: "高技术壁垒",    bottom: "低技术壁垒" }
);
slide.addImage({ data: matrix, x: 0.45, y: 1.1, w: 4.4, h: 3.8 });
```

## 5 种页面类型

### Cover（封面）

深色背景。左侧大标题，右侧几何装饰（用 `theme.secondary` 颜色的矩形色块叠加，模拟科技感分割线）。

```javascript
// 背景
slide.background = { color: theme.bg };

// 左侧竖向强调色条（装饰性）
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0, y: 0, w: 0.12, h: 5.625,
  fill: { color: theme.secondary }
});

// 主标题
slide.addText("产品名称", {
  x: 0.45, y: 1.4, w: 6.0, h: 1.1,
  fontSize: 44, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true, align: "left", margin: 0
});

// 副标题
slide.addText("副标题 / 场景说明", {
  x: 0.45, y: 2.65, w: 6.0, h: 0.5,
  fontSize: 18, fontFace: "Microsoft YaHei",
  color: theme.secondary, align: "left", margin: 0
});

// 日期 / 部门
slide.addText("2025年  ·  产品部", {
  x: 0.45, y: 4.8, w: 4.0, h: 0.3,
  fontSize: 12, fontFace: "Microsoft YaHei",
  color: theme.mutedText, align: "left", margin: 0
});
```

### Cover 精装版（推荐默认使用）

**`createRichCover` — 暗黑科技封面精装版。** 深色背景 + 左侧竖向强调色条 + 右侧 3 个发光科技感 KPI 卡，配合几何装饰块营造前沿感。

```javascript
/**
 * @param {string} title      - 产品/技术名称（白色大字）
 * @param {string} subtitle   - 副标题（青绿色）
 * @param {string} dateStr    - 日期/部门
 * @param {Array}  stats      - 右侧 3 个科技数据，每项 { value, unit, label }
 *                              例：[{ value:"99.9%", unit:"", label:"系统可用性 SLA" }, ...]
 * @param {string} tagBadge   - 左上角徽章文字（如"BETA"、"V2.0"），可选
 */
function createRichCover(pres, theme, title, subtitle, dateStr, stats, tagBadge) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧竖向青绿主色条
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 0, w: 0.14, h: 5.625, fill: { color: theme.secondary } });
  // 右侧竖向电光蓝装饰条（细）
  slide.addShape(pres.shapes.RECTANGLE, { x: 5.9, y: 0, w: 0.04, h: 5.625, fill: { color: theme.accent } });
  // 底部全宽细线
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 5.48, w: 10, h: 0.04, fill: { color: theme.secondary } });

  // 左上角 Tag Badge（可选）
  if (tagBadge) {
    slide.addShape(pres.shapes.RECTANGLE, { x: 0.3, y: 0.22, w: 1.4, h: 0.38, fill: { color: theme.secondary } });
    slide.addText(tagBadge, { x: 0.3, y: 0.22, w: 1.4, h: 0.38, fontSize: 12, fontFace: "Arial Black", color: theme.bg, bold: true, align: "center", valign: "middle", margin: 0 });
  }

  // 主标题
  slide.addText(title, {
    x: 0.3, y: 1.2, w: 5.3, h: 1.8,
    fontSize: 42, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "top", margin: 0, lineSpaceMult: 1.2
  });
  // 电光蓝下划装饰线
  slide.addShape(pres.shapes.RECTANGLE, { x: 0.3, y: 3.1, w: 2.2, h: 0.04, fill: { color: theme.accent } });

  // 副标题
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.3, y: 3.22, w: 5.3, h: 0.5,
      fontSize: 17, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "left", margin: 0
    });
  }

  // 日期/部门
  if (dateStr) {
    slide.addText(dateStr, {
      x: 0.3, y: 5.12, w: 4.0, h: 0.28,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  // ── 右侧：3 个科技 KPI 卡 ─────────────────────────────────
  const cardW = 3.72, cardH = 1.58, cardX = 6.1;
  const cardYArr = [0.28, 2.02, 3.76];

  (stats || []).slice(0, 3).forEach((s, i) => {
    const cy = cardYArr[i];
    const isFirst = i === 0;
    const accentC = isFirst ? theme.secondary : theme.accent;

    // 卡片背景
    slide.addShape(pres.shapes.RECTANGLE, { x: cardX, y: cy, w: cardW, h: cardH, fill: { color: theme.light }, line: { color: accentC, width: 0.6 } });
    // 顶部色条
    slide.addShape(pres.shapes.RECTANGLE, { x: cardX, y: cy, w: cardW, h: 0.06, fill: { color: accentC } });

    // 大数值
    slide.addText(s.value, {
      x: cardX + 0.12, y: cy + 0.1, w: cardW - 0.24, h: 0.95,
      fontSize: 38, fontFace: "Arial Black",
      color: accentC, bold: true,
      align: "center", valign: "middle", margin: 0
    });
    // 单位
    if (s.unit) {
      slide.addText(s.unit, { x: cardX + cardW * 0.55, y: cy + 0.14, w: cardW * 0.42, h: 0.28, fontSize: 13, fontFace: "Arial Black", color: accentC, bold: true, align: "left", margin: 0 });
    }
    // 标签
    slide.addText(s.label, {
      x: cardX + 0.12, y: cy + 1.1, w: cardW - 0.24, h: 0.4,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "center", margin: 0
    });
  });

  return slide;
}
```

**调用示例：**
```javascript
createRichCover(pres, theme,
  "AI 推理加速引擎\nNovaCore 2.0",
  "重新定义边缘计算的边界",
  "2025年 04月  ·  AI 基础设施部",
  [
    { value: "99.9%", unit: "", label: "系统可用性 SLA" },
    { value: "3ms",   unit: "",  label: "端到端推理延迟" },
    { value: "10×",  unit: "",  label: "较上代性能提升" },
  ],
  "V2.0"
);
```

### TOC（目录）

左半区：大标题"目录"；右半区：用 `addTOCItem` 列条目。背景 `theme.bg`。

```javascript
function createTOCSlide(pres, theme, chapters, slideNum) {
  // chapters: [{ num?, title, desc? }]
  // ≤4 章节单列，5-6 章节双列
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };           // 深色背景

  // 左侧标题区：白色大字"目录"
  slide.addText("目录", {
    x: 0.45, y: 1.6, w: 1.6, h: 0.9,
    fontSize: 34, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 青绿色"CONTENTS"小字
  slide.addText("CONTENTS", {
    x: 0.45, y: 2.55, w: 1.6, h: 0.30,
    fontSize: 11, fontFace: "Arial",
    color: theme.secondary, align: "left", margin: 0
  });

  // 左侧细竖线分隔（青绿色）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 2.2, y: 1.1, w: 0.04, h: 3.6,
    fill: { color: theme.secondary }
  });

  // 根据章节数决定布局：≤4 单列，5-6 双列
  const useTwoCol = chapters.length >= 5;

  if (useTwoCol) {
    // 双列：每列最多 3 条，行高 0.8"
    const itemH = 0.8;
    const col1X = 2.4, col2X = 6.1;
    const startY = 1.1;
    chapters.forEach((ch, i) => {
      const col = i < 3 ? 0 : 1;
      const row = i < 3 ? i : i - 3;
      const x = col === 0 ? col1X : col2X;
      const y = startY + row * itemH;
      const maxW = 3.5;
      addTOCItem(slide, pres, theme, x, y, ch.num || i + 1, ch.title, ch.desc || "", maxW);
    });
  } else {
    // 单列：行高 0.9"，最多 4 条
    const itemH = 0.9;
    const startY = 1.05;
    chapters.forEach((ch, i) => {
      const y = startY + i * itemH;
      addTOCItem(slide, pres, theme, 2.4, y, ch.num || i + 1, ch.title, ch.desc || "");
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
createTOCSlide(pres, theme, [
  { title: "技术现状",  desc: "架构痛点与性能瓶颈" },
  { title: "产品能力",  desc: "核心功能与差异化优势" },
  { title: "数据成效",  desc: "关键指标与增长曲线" },
  { title: "演进路线",  desc: "分阶段技术路线图" },
], 2);
```

### Section Divider（章节分隔）

使用 `createSectionDividerSlide` 函数，背景 `theme.dividerBg`。

### Content（内容页）

背景统一 `theme.bg`，标题用 `addSlideTitleWithAccent`，页码用 `addPageBadge`。

根据内容关系选择以下布局：

| 内容关系 | 布局 |
|----------|------|
| 并列特性 3–4 条 | 左侧图示区 + 右侧 `addFeatureItem` 列表 |
| KPI / 成效数据 | 2×2 `addKPICard` 宫格 |
| 步骤流程 | 横向 `addProcessStep` |
| 对比 | 两列卡片，左右各用 `theme.light` 背景块 |
| 纯文字要点 | 无卡片，直接 `addText` 分行，每条前加青绿方块装饰 |
| 数据趋势 / 成效展示 | `createFullDarkChartSlide`（LINE/BAR） |
| 数据 + 洞察 | `createDarkChartSlide`（左图右文） |
| 能力 / 进度展示 | `makeProgressRing` SVG |
| 技术路线图 | `makeDarkTimeline` SVG |
| 技术架构层级 | `makeDarkPyramid` SVG |
| 技术漏斗 / 管道 | `makeDarkFunnel` SVG |
| 产品 / 竞争定位 | `makeDark2x2Matrix` SVG |

### Summary（总结 / 结尾页）

深色背景，顶部青绿装饰线，大号引号装饰，白色大字核心结论 + 电光蓝分隔线 + 青绿圆点 CTA 条目。

```javascript
function createDarkSummarySlide(pres, theme, conclusion, cta, slideNum) {
  // conclusion: string — 核心结论（一句话）
  // cta: [{ text }] — 1-3 条行动召唤 / 联系信息
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };           // 深色背景

  // 顶部青绿细线装饰
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.06,
    fill: { color: theme.secondary }
  });

  // 大号青绿引号（装饰，左上角，高透明度）
  slide.addText("\u201C", {
    x: 0.3, y: 0.3, w: 1.2, h: 1.2,
    fontSize: 80, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "left", valign: "top", margin: 0,
    transparency: 70                              // 70% 透明度，仅作装饰
  });

  // 核心结论：白色大字，居左
  slide.addText(conclusion, {
    x: 0.6, y: 1.1, w: 8.8, h: 1.5,
    fontSize: 26, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "top", margin: 0
  });

  // 电光蓝水平分隔线
  slide.addShape(pres.shapes.LINE, {
    x: 0.6, y: 2.75, w: 8.8, h: 0,
    line: { color: theme.accent, width: 1 }
  });

  // CTA 条目（青绿圆点前缀 + bodyText 颜色文字）
  const ctaStartY = 3.0;
  const ctaH = Math.min(0.60, 1.8 / Math.max((cta || []).length, 1));
  (cta || []).slice(0, 3).forEach((item, i) => {
    const cy = ctaStartY + i * ctaH;
    // 青绿色圆点前缀
    slide.addShape(pres.shapes.OVAL, {
      x: 0.6, y: cy + ctaH / 2 - 0.1, w: 0.20, h: 0.20,
      fill: { color: theme.secondary }
    });
    // 条目文字（浅灰白）
    slide.addText(item.text, {
      x: 0.96, y: cy, w: 8.5, h: ctaH,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.bodyText, align: "left", valign: "middle", margin: 0
    });
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
createDarkSummarySlide(pres, theme,
  "AI 能力平台已覆盖核心业务场景，三年内可将研发效率提升 40% 并降低运营成本 30%",
  [
    { text: "扫码体验产品 Demo 或预约一对一技术沟通" },
    { text: "联系商务团队获取定制化解决方案报价" },
    { text: "关注官方渠道获取最新技术动态与白皮书" },
  ],
  12
);
```

## 视觉选择决策树

根据内容类型快速定位可用组件，深色风格所有图表必须使用 `addDarkChart` 而非普通图表函数，确保 `chartArea` 背景色正确。

| 内容类型 | 推荐组件 | 备注 |
|----------|----------|------|
| 核心指标 / 大数字 | `addKPICard` | 深色卡片，左侧强调色竖条 |
| 指标 + 趋势线 | `addKPICard` + `makeSparkline` | 趋势线颜色传 `00C9A7` 或 `4FC3F7` |
| 完成率 / 目标达成 | `makeProgressRing` | fgColor=`00C9A7`, bgColor=`1E3A4F` |
| 数据趋势（单一焦点） | `createFullDarkChartSlide`（LINE） | 全宽图表，深色 chartArea |
| 数据趋势 + 洞察 | `createDarkChartSlide`（LINE） | 左图右文，最多 3 条洞察 |
| 类别对比 | `createFullDarkChartSlide`（BAR） | 深色 chartArea，轴标签浅色 |
| 占比 / 构成 | `createFullDarkChartSlide`（PIE/DOUGHNUT） | 深色 chartArea |
| 并列特性 / 优势 | `addFeatureItem` 列表 | 青绿圆圈序号，白色标题 |
| 步骤 / 流程 | `addProcessStep` 横排 | 青绿节点，深色背景 |
| 技术路线图 / 里程碑 | `makeDarkTimeline` SVG | 青绿已完成，电光蓝当前 + 发光环 |
| 技术架构层级 | `makeDarkPyramid` SVG | 深色层级，青绿分隔线 |
| 转化漏斗 / 技术管道 | `makeDarkFunnel` SVG | 深色阶梯，顶部青绿强调条 |
| 产品定位 / 竞争分析 | `makeDark2x2Matrix` SVG | 高亮象限用青绿，电光蓝坐标轴 |
| 章节分隔 | `createSectionDividerSlide` | 极深背景，水印大数字 + 胶囊标签 |
| 目录 | `createTOCSlide` | 深色背景，青绿竖线，自适应单/双列 |
| 总结 / 结尾 | `createDarkSummarySlide` | 深色背景，引号装饰，青绿圆点 CTA |

## Dark Tech 专项规则

**颜色与对比度规则：**
- 所有图表必须使用 `addDarkChart`，`chartArea` 背景色设为 `theme.bg`（深色），禁止使用普通图表函数（否则图表区域显示白色背景，与深色幻灯片不协调）
- 轴标签颜色必须为 `theme.bodyText`（`C8D6E5`），在深背景下可见
- 网格线颜色使用 `theme.border`（`1E3A4F`），深色不抢占视觉焦点
- SVG 图形中文字颜色必须为白色（`FFFFFF`）或浅灰白（`C8D6E5`），禁止使用深色文字

**强调色使用规则：**
- 青绿（`00C9A7`）：主强调色，用于完成状态、进度、序号、CTA 前缀、分隔线
- 电光蓝（`4FC3F7`）：次强调色，用于当前状态、坐标轴、副标题下划线
- 两种强调色不在同一个元素上叠用，避免视觉混乱

**布局坐标约束：**
- 所有元素满足 `x + w ≤ 10` 且 `y + h ≤ 5.625`
- 内容安全区：`x ≥ 0.45`，`y ≥ 1.05`，`x + w ≤ 9.55`，`y + h ≤ 5.0`
- 页码徽章固定在 `x: 9.3, y: 5.1`，不占内容区空间

**信息密度规则：**
- 每张内容页一个核心观点，3–5 个支撑点
- 纯视觉叙事页（如 KPI 宫格、时间轴）允许文字极少，视觉冲击优先
- 避免超过 5 行纯文字段落，优先用卡片或图形替代
