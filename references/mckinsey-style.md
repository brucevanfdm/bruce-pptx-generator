# Style Preset: 麦肯锡蓝（McKinsey）

适合场景：战略汇报、管理层提案、咨询报告、年度规划、执行委员会演示。追求专业、权威、逻辑清晰的顾问级视觉风格。

## 核心设计哲学

**麦肯锡风格 = 结论先行 × 逻辑严密 × 视觉克制**

三大原则：
1. **Action Title（行动标题）** — 每张幻灯片的标题必须是一句完整的结论或行动建议，而非描述性话题标题。例："数字化转型可降低运营成本 35%" 而非 "数字化转型"。
2. **金字塔原则（Pyramid Principle）** — 先结论后支撑。封面页即传递核心观点，后续页面逐层展开证据。
3. **MECE** — 每张内容页的要点必须互相独立、合计完整（Mutually Exclusive, Collectively Exhaustive）。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深海蓝 | `1F3864` | 标题栏背景、主要文字 |
| `secondary` | 商务蓝 | `2E5DA8` | 副标题、强调数字、图标 |
| `accent` | 天蓝 | `4472C4` | 标题横线、卡片顶线、高亮 |
| `light` | 极浅蓝 | `EBF3FB` | 卡片背景、斑马行、浅色区 |
| `bg` | 纯白 | `FFFFFF` | 所有内容页背景 |
| `dividerBg` | 深海蓝 | `1F3864` | 章节分隔页背景（深色版） |
| `bodyText` | 深炭 | `262626` | 正文段落 |
| `mutedText` | 中灰 | `595959` | 次级文字、说明、来源注释 |
| `headerText` | 纯白 | `FFFFFF` | 标题栏白色文字 |
| `border` | 浅蓝灰 | `BDD7EE` | 表格边框、卡片边框 |

```javascript
const theme = {
  primary:    "1F3864",
  secondary:  "2E5DA8",
  accent:     "4472C4",
  light:      "EBF3FB",
  bg:         "FFFFFF",
  dividerBg:  "1F3864",
  bodyText:   "262626",
  mutedText:  "595959",
  headerText: "FFFFFF",
  border:     "BDD7EE",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 32–40 | Bold | `headerText`（白色，深蓝底） |
| 封面副标题 | Microsoft YaHei | 14–16 | Regular | `light` |
| 内容页 Action Title | Microsoft YaHei | 20–24 | Bold | `primary` |
| 二级标题 / 卡片标题 | Microsoft YaHei | 14–16 | Bold | `primary` |
| 三级标题 | Microsoft YaHei | 12–13 | Bold | `secondary` |
| 正文 | Microsoft YaHei | 11–12 | Regular | `bodyText` |
| 说明 / 来源 | Microsoft YaHei | 9–10 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 44–56 | Bold | `secondary` 或 `accent` |
| 表格表头 | Microsoft YaHei | 11–12 | Bold | `headerText`（`primary` 底） |
| 表格内容 | Microsoft YaHei | 10–11 | Regular | `bodyText` |

## 布局网格系统

幻灯片尺寸 10" × 5.625"。

**安全边界：**
- 左/右边距：`0.4"`
- 上边距（标题区以下）：`1.1"`
- 下边距：`0.3"`（页码区）
- 内容安全区：`x: 0.4–9.6`, `y: 1.1–5.3`

**麦肯锡风特有间距规范：**
- 标题区：深蓝色标题栏（全宽）+ Action Title 文字
- 内容区：严格网格对齐，列间距 ≥ 0.2"
- 表格：斑马行增强可读性
- 数据注释：左下角或底部，灰色小字

**内容密度指引（顾问汇报型）：**

> 本风格定位为**顾问汇报型**：每张幻灯片一个核心论点，3–5 条 MECE 支撑。

- 每张内容页：核心要点 3–5 条（不超过）
- 每条要点：主标题 ≤ 25 字 + 可选支撑说明 1–2 行
- 数据表格：最多 6 行 × 5 列（超出则拆页）
- 标题：必须是结论句 / 建议句，不允许纯描述性话题

## 标志性设计元素

### 1. 标题栏 + Action Title（所有非封面页必用）

麦肯锡标志：全宽深蓝标题栏，白色 Action Title 文字。

```javascript
function addMcKinseySlideTitle(slide, pres, theme, title, source) {
  // 深蓝标题栏（全宽）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.9,
    fill: { color: theme.primary }
  });
  // Action Title（白色）
  slide.addText(title, {
    x: 0.4, y: 0, w: 9.2, h: 0.9,
    fontSize: 22, fontFace: "Microsoft YaHei",
    color: theme.headerText, bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 来源注释（可选，左下角小灰字）
  if (source) {
    slide.addText(`来源：${source}`, {
      x: 0.4, y: 5.3, w: 6, h: 0.25,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }
}
```

### 2. 页码徽章（所有非封面页必用）

```javascript
function addPageBadge(slide, pres, theme, num) {
  // 麦肯锡风：深蓝矩形，右下角
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 9.2, y: 5.1, w: 0.55, h: 0.35,
    fill: { color: theme.primary }
  });
  slide.addText(String(num), {
    x: 9.2, y: 5.1, w: 0.55, h: 0.35,
    fontSize: 11, fontFace: "Arial", color: theme.headerText,
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. 数据表格（斑马行）

```javascript
function addMcKinseyTable(slide, pres, theme, x, y, w, h, headers, rows) {
  const colW = w / headers.length;
  const rowH = (h - 0.45) / rows.length; // 0.45 = 表头高度

  // 表头行
  headers.forEach((header, i) => {
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + i * colW, y: y, w: colW, h: 0.45,
      fill: { color: theme.primary }
    });
    slide.addText(header, {
      x: x + i * colW + 0.08, y: y, w: colW - 0.16, h: 0.45,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.headerText, bold: true,
      align: i === 0 ? "left" : "center", valign: "middle", margin: 0
    });
  });

  // 数据行（斑马行）
  rows.forEach((row, ri) => {
    const rowY = y + 0.45 + ri * rowH;
    const isEven = ri % 2 === 0;
    row.forEach((cell, ci) => {
      if (isEven) {
        slide.addShape(pres.shapes.RECTANGLE, {
          x: x + ci * colW, y: rowY, w: colW, h: rowH,
          fill: { color: theme.light }
        });
      }
      slide.addText(cell, {
        x: x + ci * colW + 0.08, y: rowY, w: colW - 0.16, h: rowH,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.bodyText,
        align: ci === 0 ? "left" : "center", valign: "middle", margin: 0
      });
    });
  });
}
```

### 4. 分析卡片（KPI / 结论卡）

```javascript
function addMcKinseyCard(slide, pres, theme, x, y, w, h, value, label, description) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h,
    fill: { color: theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 顶部蓝色强调线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.05,
    fill: { color: theme.accent }
  });
  // 核心数值
  slide.addText(value, {
    x: x + 0.15, y: y + 0.2, w: w - 0.3, h: 0.8,
    fontSize: 44, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + 1.05, w: w - 0.2, h: 0.35,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "center", margin: 0
  });
  // 说明
  if (description) {
    slide.addText(description, {
      x: x + 0.1, y: y + 1.4, w: w - 0.2, h: 0.4,
      fontSize: 10, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "center", margin: 0
    });
  }
}
```

### 5. 要点列表（带层级缩进）

```javascript
function addBulletSection(slide, pres, theme, x, y, w, items) {
  // items: [{ text, level, bold }]  level: 0=主要, 1=次级
  let curY = y;
  items.forEach(item => {
    const isMain = item.level === 0;
    const indent = isMain ? 0 : 0.3;
    const fs = isMain ? 13 : 11;
    const dotColor = isMain ? theme.accent : theme.secondary;
    const lineH = isMain ? 0.36 : 0.3;
    const gap = isMain ? 0.12 : 0.08;

    // 蓝色方块前缀
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + indent, y: curY + (lineH - 0.1) / 2, w: 0.1, h: 0.1,
      fill: { color: dotColor }
    });
    slide.addText(item.text, {
      x: x + indent + 0.18, y: curY, w: w - indent - 0.18, h: lineH,
      fontSize: fs, fontFace: "Microsoft YaHei",
      color: isMain ? theme.bodyText : theme.mutedText,
      bold: item.bold || false,
      align: "left", valign: "middle", margin: 0
    });
    curY += lineH + gap;
  });
}
```

### 6. 章节分隔页

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg }; // 深海蓝

  // 左侧亮蓝竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.55, y: 1.2, w: 0.08, h: 3.2,
    fill: { color: theme.accent }
  });
  // 章节编号（大字，半透明白）
  slide.addText(String(num).padStart(2, '0'), {
    x: 0.8, y: 0.8, w: 3.5, h: 2.0,
    fontSize: 120, fontFace: "Arial Black",
    color: "FFFFFF", bold: true,
    align: "left", margin: 0,
    transparency: 85
  });
  // 章节标题（白色）
  slide.addText(title, {
    x: 0.8, y: 2.7, w: 8.0, h: 0.8,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });
  // 副标题
  slide.addText(subtitle, {
    x: 0.8, y: 3.55, w: 8.0, h: 0.4,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: theme.light, align: "left", margin: 0
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 7. 图表（数据可视化）

**图表必须承载数据洞察，搭配 Action Title 传达结论，不作纯装饰。**

```javascript
// 麦肯锡色板图表基础函数
function addMcKinseyChart(slide, pres, theme, type, chartData, opts = {}) {
  const defaults = {
    chartColors: [theme.secondary, theme.accent, "6B9FD4", "9DBFE8"],
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

**图表 + 右侧洞察布局（左 60% 图表 + 右 40% MECE 洞察）：**

```javascript
function createChartWithInsightsSlide(pres, theme, title, chartData, chartType, insights, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addMcKinseySlideTitle(slide, pres, theme, title, source);

  // 左侧图表区
  addMcKinseyChart(slide, pres, theme, chartType, chartData, {
    x: 0.4, y: 1.05, w: 5.8, h: 3.9,
    barDir: "col",
    dataLabelPosition: "outEnd",
  });

  // 右侧分隔线
  slide.addShape(pres.shapes.LINE, {
    x: 6.4, y: 1.15, w: 0, h: 3.7,
    line: { color: theme.border, width: 0.75 }
  });

  // 右侧洞察要点（最多 3 条）
  insights.slice(0, 3).forEach((item, i) => {
    const iy = 1.2 + i * 1.3;
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 6.6, y: iy, w: 0.32, h: 0.32,
      fill: { color: theme.accent }
    });
    slide.addText(String(i + 1), {
      x: 6.6, y: iy, w: 0.32, h: 0.32,
      fontSize: 12, fontFace: "Arial", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    slide.addText(item.title, {
      x: 7.05, y: iy, w: 2.5, h: 0.32,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    if (item.desc) {
      slide.addText(item.desc, {
        x: 7.05, y: iy + 0.35, w: 2.5, h: 0.7,
        fontSize: 10, fontFace: "Microsoft YaHei",
        color: theme.mutedText, align: "left", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**全宽图表页（主视觉数据页）：**

```javascript
function createFullChartSlide(pres, theme, title, chartData, chartType, source, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addMcKinseySlideTitle(slide, pres, theme, title, source);

  addMcKinseyChart(slide, pres, theme, chartType, chartData, {
    x: 0.4, y: 1.05, w: 9.2, h: 3.9,
    barDir: "col",
    dataLabelPosition: "outEnd",
    showLegend: chartData.length > 1,
    legendPos: "b",
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 8. 图标卡片（Icon + KPI）

**使用 react-icons 图标增强 KPI 卡，视觉层级更清晰。图标必须与指标语义相关。**

安装依赖（全局）：
```shell
npm install -g react-icons react react-dom sharp
```

**icon-utils.js（在项目目录创建一次）：**

```javascript
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

**compile.js——使用图标时，整个文件必须包裹在 async IIFE 内：**

```javascript
const pptxgen = require("pptxgenjs");
const fs = require("fs");
const path = require("path");
const { iconToBase64Png } = require("./icon-utils");
const { FaChartBar, FaUsers, FaShieldAlt, FaClock, FaBullseye } = require("react-icons/fa");
const { MdTrendingUp, MdBusiness } = require("react-icons/md");

// CommonJS 不支持顶层 await，必须用 async IIFE 包裹整个编译逻辑
(async () => {
  const pres = new pptxgen();
  pres.layout = "LAYOUT_16x9";

  const theme = { /* 替换为当前预设调色板 */ };

  // 在 for 循环之前预生成所有图标（iconToBase64Png 颜色参数无需带 #）
  const icons = {};
  icons.chartBar = await iconToBase64Png(FaChartBar,  "2E5DA8", 256);
  icons.users    = await iconToBase64Png(FaUsers,     "2E5DA8", 256);
  icons.shield   = await iconToBase64Png(FaShieldAlt, "4472C4", 256);
  icons.clock    = await iconToBase64Png(FaClock,     "2E5DA8", 256);
  icons.target   = await iconToBase64Png(FaBullseye,  "4472C4", 256);
  icons.trending = await iconToBase64Png(MdTrendingUp,"2E5DA8", 256);

  // 按顺序加载幻灯片文件，传入 icons
  const slideFiles = fs.readdirSync(__dirname)
    .filter(f => /^slide-\d+\.js$/.test(f))
    .sort();

  for (const file of slideFiles) {
    const mod = require(path.join(__dirname, file));
    mod.createSlide(pres, theme, { icons });
  }

  fs.mkdirSync(path.join(__dirname, "output"), { recursive: true });
  await pres.writeFile({ fileName: path.join(__dirname, "output", "presentation.pptx") });
  console.log("Done → slides/output/presentation.pptx");
})();
```

**带图标的 KPI 卡函数（h 建议 2.2）：**

```javascript
function addIconKpiCard(slide, pres, theme, x, y, w, h, iconData, value, label, desc) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h,
    fill: { color: theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 顶部强调线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.05,
    fill: { color: theme.accent }
  });
  // 图标（居中，顶部区域）
  if (iconData) {
    const iconSize = 0.45;
    slide.addImage({
      data: iconData,
      x: x + (w - iconSize) / 2, y: y + 0.18,
      w: iconSize, h: iconSize
    });
  }
  // KPI 大数字
  slide.addText(value, {
    x: x + 0.1, y: y + 0.72, w: w - 0.2, h: 0.65,
    fontSize: 36, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + 1.42, w: w - 0.2, h: 0.35,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "center", margin: 0
  });
  // 说明
  if (desc) {
    slide.addText(desc, {
      x: x + 0.1, y: y + 1.8, w: w - 0.2, h: 0.3,
      fontSize: 9, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "center", margin: 0
    });
  }
}
```

### 9. SVG 内联图形（零依赖，完全同步）

无需任何外部库。在 Node.js 生成 SVG 字符串，转 base64 嵌入幻灯片。适用于图表库无法满足的自定义可视化。

```javascript
function svgToBase64(svgStr) {
  return "image/svg+xml;base64," + Buffer.from(svgStr).toString("base64");
}
```

**进度环（完成率 / 目标达成 / 覆盖率）：**

```javascript
function makeProgressRing(percent, fgColor, bgColor, label = "完成率", size = 200) {
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
        font-size="16" font-family="Arial" fill="#595959">${label}</text>
    </svg>
  `);
}
// 用法
const ring = makeProgressRing(75, "2E5DA8", "BDD7EE", "达成率");
slide.addImage({ data: ring, x: 1.2, y: 1.3, w: 1.4, h: 1.4 });
```

**水平对比条（各维度评分 / 市场份额对比）：**

```javascript
function makeHBarChart(items, barColor, bgColor, chartW = 400) {
  const barH = 22, gap = 12, labelW = 90, maxBarW = chartW - labelW - 55;
  const maxVal = Math.max(...items.map(d => d.value));
  const rows = items.map((d, i) => {
    const y = i * (barH + gap) + 16;
    const bw = Math.round((d.value / maxVal) * maxBarW);
    return `
      <text x="0" y="${y + barH * 0.72}" font-size="13" font-family="Arial" fill="#595959">${d.label}</text>
      <rect x="${labelW}" y="${y}" width="${maxBarW}" height="${barH}" rx="3" fill="#${bgColor}"/>
      <rect x="${labelW}" y="${y}" width="${bw}" height="${barH}" rx="3" fill="#${barColor}"/>
      <text x="${labelW + bw + 8}" y="${y + barH * 0.72}" font-size="13" font-family="Arial Black" fill="#${barColor}">${d.value}${d.unit || ""}</text>
    `;
  }).join("");
  const svgH = items.length * (barH + gap) + 20;
  return svgToBase64(`<svg width="${chartW}" height="${svgH}" xmlns="http://www.w3.org/2000/svg">${rows}</svg>`);
}
// 用法
const hbar = makeHBarChart([
  { label: "产品A", value: 85, unit: "%" },
  { label: "产品B", value: 62, unit: "%" },
  { label: "产品C", value: 47, unit: "%" },
], "2E5DA8", "EBF3FB");
slide.addImage({ data: hbar, x: 0.4, y: 1.2, w: 5.5, h: 2.0 });
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
// 用法（KPI 卡底部趋势线）
const spark = makeSparkline([42, 55, 51, 67, 72, 80, 88], "4472C4");
slide.addImage({ data: spark, x: x + 0.15, y: y + 1.6, w: w - 0.3, h: 0.5 });
```

**流程节点（战略路径图 / 实施步骤）：**

```javascript
function makeProcessNode(num, label, fgColor, bgColor, size = 120) {
  return svgToBase64(`
    <svg width="${size}" height="${size}" xmlns="http://www.w3.org/2000/svg">
      <circle cx="${size/2}" cy="${size/2}" r="${size/2 - 4}" fill="#${bgColor}" stroke="#${fgColor}" stroke-width="3"/>
      <text x="${size/2}" y="${size/2 - 8}" text-anchor="middle"
        font-size="${Math.round(size * 0.28)}" font-weight="bold" font-family="Arial" fill="#${fgColor}">${num}</text>
      <text x="${size/2}" y="${size/2 + 18}" text-anchor="middle"
        font-size="${Math.round(size * 0.13)}" font-family="Arial" fill="#${fgColor}">${label}</text>
    </svg>
  `);
}
// 用法（3 步流程，节点间加连接箭头 LINE）
const node1 = makeProcessNode("01", "诊断", "1F3864", "EBF3FB");
slide.addImage({ data: node1, x: 0.5, y: 1.8, w: 1.1, h: 1.1 });
```

**金字塔图（层级结构 / 价值模型 / 能力模型）：**

```javascript
function makePyramid(layers, colors, w = 500, h = 360) {
  // layers: [{ label, value? }]，顺序从顶到底（顶层最窄）
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
        font-size="${Math.round(fs * 0.78)}" font-family="Arial" fill="rgba(255,255,255,0.85)">${layer.value}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">${shapes.join("")}</svg>`);
}
// 用法（4 层能力模型）
const pyramid = makePyramid([
  { label: "战略目标" },
  { label: "核心能力",  value: "差异化" },
  { label: "执行体系",  value: "流程+人才" },
  { label: "基础支撑",  value: "数据+技术" },
], ["1F3864", "2E5DA8", "4472C4", "6B9FD4"]);
slide.addImage({ data: pyramid, x: 0.5, y: 1.1, w: 4.8, h: 3.5 });
```

**漏斗图（转化分析 / 业务管道 / 阶段流程）：**

```javascript
function makeFunnel(stages, colors, w = 400, h = 320) {
  // stages: [{ label, value, rate? }]，顺序从上到下（顶层最宽）
  // colors: 颜色数组，不足时循环使用
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
    return `
      <polygon points="${pts}" fill="#${color}"/>
      <text x="${cx}" y="${textY - fs * 0.3}" text-anchor="middle"
        font-size="${fs}" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${stage.label}</text>
      <text x="${cx}" y="${textY + fs * 0.9}" text-anchor="middle"
        font-size="${Math.round(fs * 0.88)}" font-family="Arial Black" fill="rgba(255,255,255,0.9)">${stage.value}</text>
      ${stage.rate ? `<text x="${rateX}" y="${textY + 4}" font-size="11" font-family="Arial" fill="#595959">${stage.rate}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">${shapes.join("")}</svg>`);
}
// 用法（4 阶段销售漏斗）
const funnel = makeFunnel([
  { label: "线索",   value: "12,400", rate: "100%" },
  { label: "意向",   value: "4,800",  rate: "39%" },
  { label: "报价",   value: "1,560",  rate: "13%" },
  { label: "成交",   value: "420",    rate: "3.4%" },
], ["1F3864", "2E5DA8", "4472C4", "6B9FD4"]);
slide.addImage({ data: funnel, x: 0.5, y: 1.1, w: 4.0, h: 3.5 });
```

**2×2 矩阵（优先级矩阵 / BCG 矩阵 / 影响力分析）：**

```javascript
function make2x2Matrix(quadrants, xAxis, yAxis, w = 440, h = 380) {
  // quadrants: [TL, TR, BL, BR]，每项 { label, sublabel, color? }
  // xAxis: { left, right }，yAxis: { top, bottom }
  const pad = 44, qw = (w - pad * 2) / 2, qh = (h - pad * 2) / 2;
  const defaultColors = ["EBF3FB", "2E5DA8", "4472C4", "EBF3FB"];
  const positions = [
    { row: 0, col: 0 }, { row: 0, col: 1 },
    { row: 1, col: 0 }, { row: 1, col: 1 },
  ];

  const quads = quadrants.map((q, i) => {
    const { row, col } = positions[i];
    const x = pad + col * qw, y = pad + row * qh;
    const bg = q.color || defaultColors[i];
    const isDark = ["1F3864", "2E5DA8", "4472C4"].includes(bg);
    const textColor = isDark ? "FFFFFF" : "1F3864";
    const subColor  = isDark ? "BDD7EE" : "595959";
    return `
      <rect x="${x}" y="${y}" width="${qw}" height="${qh}" fill="#${bg}" stroke="white" stroke-width="2"/>
      <text x="${(x + qw / 2).toFixed(1)}" y="${(y + qh / 2 - 8).toFixed(1)}" text-anchor="middle"
        font-size="15" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="#${textColor}">${q.label}</text>
      ${q.sublabel ? `<text x="${(x + qw / 2).toFixed(1)}" y="${(y + qh / 2 + 14).toFixed(1)}" text-anchor="middle"
        font-size="11" font-family="Microsoft YaHei,Arial" fill="#${subColor}">${q.sublabel}</text>` : ""}
    `;
  });

  // 轴线（带箭头）
  const ax = pad, ay = pad + qh, aex = pad + qw * 2, aey = pad;
  const axes = `
    <defs>
      <marker id="arh" markerWidth="7" markerHeight="7" refX="5" refY="3.5" orient="auto">
        <polygon points="0,0 7,3.5 0,7" fill="#4472C4"/>
      </marker>
    </defs>
    <line x1="${ax}" y1="${ay}" x2="${aex + 16}" y2="${ay}"
      stroke="#4472C4" stroke-width="1.5" marker-end="url(#arh)"/>
    <line x1="${pad + qw}" y1="${pad + qh * 2}" x2="${pad + qw}" y2="${aey - 16}"
      stroke="#4472C4" stroke-width="1.5" marker-end="url(#arh)"/>
  `;

  // 轴标签
  const labels = `
    <text x="${aex + 20}" y="${ay + 4}" font-size="11" font-family="Arial" fill="#2E5DA8">${xAxis?.right || ""}</text>
    <text x="${ax - 4}" y="${ay + 4}" text-anchor="end" font-size="11" font-family="Arial" fill="#595959">${xAxis?.left || ""}</text>
    <text x="${pad + qw}" y="${aey - 20}" text-anchor="middle" font-size="11" font-family="Arial" fill="#2E5DA8">${yAxis?.top || ""}</text>
    <text x="${pad + qw}" y="${pad + qh * 2 + 16}" text-anchor="middle" font-size="11" font-family="Arial" fill="#595959">${yAxis?.bottom || ""}</text>
  `;

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${axes}${quads.join("")}${labels}
  </svg>`);
}
// 用法（优先级矩阵）
const matrix = make2x2Matrix(
  [
    { label: "延后",   sublabel: "低价值·低紧急" },
    { label: "重点推进", sublabel: "高价值·高紧急", color: "1F3864" },
    { label: "搁置",   sublabel: "低价值·低紧急" },
    { label: "规划",   sublabel: "高价值·低紧急",  color: "2E5DA8" },
  ],
  { left: "低紧急", right: "高紧急" },
  { top: "高价值",  bottom: "低价值" }
);
slide.addImage({ data: matrix, x: 0.4, y: 1.1, w: 4.4, h: 3.8 });
```

**瀑布图（收入拆解 / 成本 Bridge / 同比变化分析）：**

```javascript
function makeWaterfall(items, colors, w = 520, h = 300) {
  // items: [{ label, value, type? }]  type: "total" | undefined
  // colors: { positive, negative, total }
  // 首尾 item 通常设 type:"total"，中间 item 自动为浮动条
  const n = items.length;
  const padL = 40, padB = 36, padT = 24, padR = 12;
  const chartW = w - padL - padR, chartH = h - padB - padT;
  const barW = chartW / n * 0.58, barStep = chartW / n;

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
    const color = bar.isTotal ? colors.total : (bar.isNeg ? colors.negative : colors.positive);

    const nextBar = bars[i + 1];
    const connector = nextBar && !nextBar.isTotal
      ? `<line x1="${(bx + barW).toFixed(1)}" y1="${toY(bar.top).toFixed(1)}"
               x2="${(padL + (i + 1) * barStep + (barStep - barW) / 2).toFixed(1)}" y2="${toY(bar.top).toFixed(1)}"
               stroke="#CCCCCC" stroke-width="1" stroke-dasharray="3,2"/>`
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
        font-size="11" font-family="Microsoft YaHei,Arial" fill="#595959">${bar.label}</text>
    `;
  });

  const zeroLine = `<line x1="${padL}" y1="${zeroY.toFixed(1)}" x2="${w - padR}" y2="${zeroY.toFixed(1)}"
    stroke="#BDD7EE" stroke-width="1.2"/>`;

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${zeroLine}${shapes.join("")}
  </svg>`);
}
// 用法（收入 Bridge）
const waterfall = makeWaterfall([
  { label: "去年收入", value: 850, type: "total" },
  { label: "新客增长", value: 120 },
  { label: "老客续签", value: 80  },
  { label: "客户流失", value: -60 },
  { label: "价格调整", value: -20 },
  { label: "今年收入", value: 970, type: "total" },
], { positive: "2E5DA8", negative: "C0392B", total: "1F3864" });
slide.addImage({ data: waterfall, x: 0.4, y: 1.1, w: 9.2, h: 3.5 });
```

**横向时间轴（实施路线图 / 里程碑规划）：**

```javascript
function makeTimeline(milestones, w = 860, h = 160) {
  // milestones: [{ date, title, desc?, done?, current? }]
  // done: 已完成（实心蓝点）current: 当前（大圆 + 光晕圈）future: 未来（空心点）
  const n = milestones.length;
  const padH = 50, lineY = h * 0.48;
  const step = (w - padH * 2) / Math.max(n - 1, 1);
  const currIdx = milestones.findIndex(m => m.current);

  const bgLine = `<line x1="${padH}" y1="${lineY}" x2="${w - padH}" y2="${lineY}"
    stroke="#BDD7EE" stroke-width="2.5"/>`;
  const progressLine = currIdx > 0
    ? `<line x1="${padH}" y1="${lineY}" x2="${(padH + currIdx * step).toFixed(1)}" y2="${lineY}"
        stroke="#2E5DA8" stroke-width="2.5"/>`
    : "";

  const nodes = milestones.map((m, i) => {
    const x = padH + i * step;
    const isDone = m.done || (currIdx >= 0 && i < currIdx);
    const isCurrent = m.current;
    const r = isCurrent ? 10 : 7;
    const fill = isDone ? "2E5DA8" : (isCurrent ? "1F3864" : "FFFFFF");
    const stroke = isDone || isCurrent ? "2E5DA8" : "BDD7EE";
    const sw = isCurrent ? 3 : 2;
    const ring = isCurrent
      ? `<circle cx="${x.toFixed(1)}" cy="${lineY}" r="16"
           fill="none" stroke="#4472C4" stroke-width="1.5" opacity="0.45"/>`
      : "";
    return `
      ${ring}
      <circle cx="${x.toFixed(1)}" cy="${lineY}" r="${r}" fill="#${fill}" stroke="#${stroke}" stroke-width="${sw}"/>
      <text x="${x.toFixed(1)}" y="${(lineY - r - 7).toFixed(1)}" text-anchor="middle"
        font-size="10" font-family="Arial" fill="#595959">${m.date}</text>
      <text x="${x.toFixed(1)}" y="${(lineY + r + 16).toFixed(1)}" text-anchor="middle"
        font-size="12" font-weight="${isCurrent ? "bold" : "normal"}" font-family="Microsoft YaHei,Arial"
        fill="#${isCurrent ? "1F3864" : (isDone ? "262626" : "595959")}">${m.title}</text>
      ${m.desc ? `<text x="${x.toFixed(1)}" y="${(lineY + r + 30).toFixed(1)}" text-anchor="middle"
        font-size="10" font-family="Microsoft YaHei,Arial" fill="#595959">${m.desc}</text>` : ""}
    `;
  });

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    ${bgLine}${progressLine}${nodes.join("")}
  </svg>`);
}
// 用法（项目路线图，宽度铺满幻灯片）
const timeline = makeTimeline([
  { date: "Q1 2024", title: "诊断评估", done: true },
  { date: "Q2 2024", title: "方案设计", done: true },
  { date: "Q3 2024", title: "试点实施", current: true, desc: "进行中" },
  { date: "Q4 2024", title: "全量推广" },
  { date: "Q1 2025", title: "效果评估" },
]);
slide.addImage({ data: timeline, x: 0.4, y: 2.8, w: 9.2, h: 1.7 });
```

**维恩图（交叉关系 / 重叠分析 / 能力交集）：**

```javascript
function makeVenn(left, right, overlap, w = 420, h = 300) {
  // left/right: { label, items: ['...'] }（各显示 2 项）
  // overlap: { label, items: ['...'] }（交叉区，显示 2 项）
  const cx = w / 2, cy = h / 2;
  const r = h * 0.38, offset = r * 0.50;
  const c1x = cx - offset, c2x = cx + offset;

  const leftItems = (left.items || []).slice(0, 2).map((t, i) =>
    `<text x="${(c1x - r * 0.28).toFixed(1)}" y="${(cy + 10 + i * 18).toFixed(1)}" text-anchor="middle"
      font-size="10" font-family="Microsoft YaHei,Arial" fill="rgba(255,255,255,0.9)">${t}</text>`
  ).join("");
  const rightItems = (right.items || []).slice(0, 2).map((t, i) =>
    `<text x="${(c2x + r * 0.28).toFixed(1)}" y="${(cy + 10 + i * 18).toFixed(1)}" text-anchor="middle"
      font-size="10" font-family="Microsoft YaHei,Arial" fill="rgba(255,255,255,0.9)">${t}</text>`
  ).join("");
  const overlapItems = (overlap.items || []).slice(0, 2).map((t, i) =>
    `<text x="${cx}" y="${(cy + 10 + i * 18).toFixed(1)}" text-anchor="middle"
      font-size="10" font-family="Microsoft YaHei,Arial" fill="rgba(255,255,255,0.9)">${t}</text>`
  ).join("");

  return svgToBase64(`<svg width="${w}" height="${h}" xmlns="http://www.w3.org/2000/svg">
    <circle cx="${c1x}" cy="${cy}" r="${r}" fill="#2E5DA8" opacity="0.78"/>
    <circle cx="${c2x}" cy="${cy}" r="${r}" fill="#4472C4" opacity="0.68"/>
    <text x="${(c1x - r * 0.28).toFixed(1)}" y="${(cy - 12).toFixed(1)}" text-anchor="middle"
      font-size="13" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${left.label}</text>
    ${leftItems}
    <text x="${(c2x + r * 0.28).toFixed(1)}" y="${(cy - 12).toFixed(1)}" text-anchor="middle"
      font-size="13" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${right.label}</text>
    ${rightItems}
    <text x="${cx}" y="${(cy - 12).toFixed(1)}" text-anchor="middle"
      font-size="12" font-weight="bold" font-family="Microsoft YaHei,Arial" fill="white">${overlap.label || ""}</text>
    ${overlapItems}
  </svg>`);
}
// 用法
const venn = makeVenn(
  { label: "技术能力",  items: ["算法研发", "系统架构"] },
  { label: "市场能力",  items: ["客户洞察", "品牌运营"] },
  { label: "核心优势",  items: ["数字化产品"] }
);
slide.addImage({ data: venn, x: 0.5, y: 1.2, w: 4.5, h: 3.2 });
```

### 10. SWOT 页面模板

四象限框架页，适合战略分析、竞争评估、项目评审。

```javascript
function createSWOTSlide(pres, theme, title, swot, source, slideNum) {
  // swot: { S: ['...'], W: ['...'], O: ['...'], T: ['...'] }  每个最多 4 条
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addMcKinseySlideTitle(slide, pres, theme, title, source);

  const defs = [
    { key: "S", label: "优势 Strengths",     color: theme.primary,   items: swot.S, col: 0, row: 0 },
    { key: "W", label: "劣势 Weaknesses",    color: theme.secondary, items: swot.W, col: 1, row: 0 },
    { key: "O", label: "机会 Opportunities", color: theme.accent,    items: swot.O, col: 0, row: 1 },
    { key: "T", label: "威胁 Threats",       color: "595959",        items: swot.T, col: 1, row: 1 },
  ];

  const qw = 4.5, qh = 1.88, startX = 0.4, startY = 1.05, gap = 0.1;
  const headerH = 0.36, itemH = 0.28;

  defs.forEach(q => {
    const x = startX + q.col * (qw + gap);
    const y = startY + q.row * (qh + gap);

    // Header bar
    slide.addShape(pres.shapes.RECTANGLE, { x, y, w: qw, h: headerH, fill: { color: q.color } });
    // S/W/O/T letter
    slide.addText(q.key, {
      x, y, w: 0.36, h: headerH,
      fontSize: 15, fontFace: "Arial Black", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    // Label
    slide.addText(q.label, {
      x: x + 0.4, y, w: qw - 0.4, h: headerH,
      fontSize: 11, fontFace: "Microsoft YaHei", color: theme.headerText,
      bold: true, align: "left", valign: "middle", margin: 0
    });
    // Content background
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: y + headerH, w: qw, h: qh - headerH,
      fill: { color: theme.light },
      line: { color: theme.border, width: 0.5 }
    });
    // Items
    let curY = y + headerH + 0.08;
    (q.items || []).slice(0, 4).forEach(item => {
      slide.addShape(pres.shapes.RECTANGLE, {
        x: x + 0.13, y: curY + 0.09, w: 0.08, h: 0.08,
        fill: { color: q.color }
      });
      slide.addText(item, {
        x: x + 0.27, y: curY, w: qw - 0.37, h: itemH,
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

### 11. 比较矩阵（多方案 / 竞品对比）

适合方案选型、竞品分析、评估报告。支持 ✓ / ✗ / ◐ 符号和文字混用。

```javascript
function addComparisonGrid(slide, pres, theme, x, y, w, h, options, features, cells) {
  // options: ['方案A', '方案B', '方案C']（最多 4 个）
  // features: ['功能1', '功能2', ...]（最多 7 条）
  // cells: 二维数组，值: 'yes' | 'no' | 'partial' | 任意文字
  const nOpts = options.length;
  const nFeat = features.length;
  const labelColW = w * 0.32;
  const optColW = (w - labelColW) / nOpts;
  const headerH = 0.38;
  const rowH = (h - headerH) / nFeat;

  // Header corner
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w: labelColW, h: headerH,
    fill: { color: theme.primary }
  });

  // Option columns header
  options.forEach((opt, i) => {
    const cx = x + labelColW + i * optColW;
    slide.addShape(pres.shapes.RECTANGLE, {
      x: cx, y, w: optColW, h: headerH,
      fill: { color: i === 0 ? theme.primary : theme.secondary }
    });
    slide.addText(opt, {
      x: cx + 0.05, y, w: optColW - 0.1, h: headerH,
      fontSize: 11, fontFace: "Microsoft YaHei", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
  });

  // Feature rows
  features.forEach((feat, ri) => {
    const ry = y + headerH + ri * rowH;
    const rowBg = ri % 2 === 0 ? theme.light : theme.bg;

    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: ry, w: labelColW, h: rowH,
      fill: { color: rowBg }
    });
    slide.addText(feat, {
      x: x + 0.12, y: ry, w: labelColW - 0.18, h: rowH,
      fontSize: 10, fontFace: "Microsoft YaHei", color: theme.primary,
      bold: true, align: "left", valign: "middle", margin: 0
    });

    options.forEach((_, ci) => {
      const cx = x + labelColW + ci * optColW;
      const val = (cells[ri] || [])[ci] || "";
      slide.addShape(pres.shapes.RECTANGLE, {
        x: cx, y: ry, w: optColW, h: rowH,
        fill: { color: rowBg },
        line: { color: theme.border, width: 0.3 }
      });
      let display = val, color = theme.bodyText, fs = 10, bold = false;
      if (val === "yes")     { display = "✓"; color = "107C41"; fs = 15; bold = true; }
      else if (val === "no") { display = "✗"; color = "C0392B"; fs = 15; bold = true; }
      else if (val === "partial") { display = "◐"; color = theme.secondary; fs = 15; bold = true; }
      slide.addText(display, {
        x: cx, y: ry, w: optColW, h: rowH,
        fontSize: fs, fontFace: fs > 10 ? "Arial" : "Microsoft YaHei",
        color, bold, align: "center", valign: "middle", margin: 0
      });
    });
  });

  // Vertical divider after label column
  slide.addShape(pres.shapes.LINE, {
    x: x + labelColW, y, w: 0, h: h,
    line: { color: theme.border, width: 0.5 }
  });
}
// 用法
addComparisonGrid(slide, pres, theme, 0.4, 1.05, 9.2, 4.2,
  ["推荐方案", "方案B", "现有方案"],
  ["实施成本", "技术复杂度", "可扩展性", "交付周期", "风险等级"],
  [
    ["低",      "中",    "高"      ],
    ["yes",     "partial","no"    ],
    ["yes",     "yes",   "no"     ],
    ["3个月",   "5个月", "8个月"  ],
    ["低",      "中",    "高"     ],
  ]
);
```

### 12. 雷达图（能力评估 / 竞争力对比）

使用 PptxGenJS 原生 RADAR 图表，适合多维度能力评分、竞争力分析。

```javascript
function addMcKinseyRadarChart(slide, pres, theme, x, y, w, h, dimensions, seriesData) {
  // dimensions: ['维度1', '维度2', ...]（建议 5–7 个）
  // seriesData: [{ name: '系列A', values: [85, 70, ...] }, ...]
  slide.addChart(pres.charts.RADAR, seriesData.map(s => ({
    name: s.name, labels: dimensions, values: s.values
  })), {
    x, y, w, h,
    radarStyle: "marker",
    chartColors: [theme.secondary, theme.accent, "6B9FD4"],
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
// 用法（能力差距分析，左侧雷达 + 右侧说明）
addMcKinseyRadarChart(slide, pres, theme, 0.4, 1.1, 5.5, 4.0,
  ["战略思维", "执行能力", "数据分析", "沟通协作", "创新意识"],
  [
    { name: "当前水平", values: [70, 85, 60, 75, 65] },
    { name: "目标水平", values: [90, 90, 85, 85, 80] },
  ]
);
```

## 视觉选择决策树

根据内容类型选择合适的视觉组件，避免全文字布局：

| 内容类型 | 推荐组件 |
|---------|---------|
| 时间序列趋势 | `addMcKinseyChart(LINE)` |
| 类别对比（5 项以内） | `addMcKinseyChart(BAR)` |
| 多维对比 + 洞察 | `createChartWithInsightsSlide` |
| 构成比例 | `addMcKinseyChart(PIE/DOUGHNUT)` |
| 多维对比条（无原生图表） | `makeHBarChart` (SVG) |
| KPI 数字 + 语义图标 | `addIconKpiCard`（react-icons） |
| 完成率 / 目标达成 | `makeProgressRing` (SVG) |
| KPI 卡内走势 | `makeSparkline` (SVG) |
| 流程 / 路径步骤 | `makeProcessNode` (SVG) + LINE |
| 层级结构 / 价值模型 | `makePyramid` (SVG) |
| 转化漏斗 / 业务管道 | `makeFunnel` (SVG) |
| 优先级 / BCG / 影响力矩阵 | `make2x2Matrix` (SVG) |
| 收入拆解 / 成本 Bridge | `makeWaterfall` (SVG) |
| 实施路线图 / 里程碑 | `makeTimeline` (SVG) |
| 交叉关系 / 重叠分析 | `makeVenn` (SVG) |
| 战略分析框架 (SWOT) | `createSWOTSlide` |
| 多方案 / 竞品对比 | `addComparisonGrid` |
| 多维能力评分 / 竞争力 | `addMcKinseyRadarChart` |
| 并列要点文字 | `addBulletSection` |

**每张 Content 页至少包含一种非纯文字的视觉组件（图表、图标卡、SVG 图形），除非内容本身是纯文字分析结论。**

## 5 种页面类型

### Cover（封面）

深蓝色左侧色带 + 白色右侧区域，标题置于左侧色带上。

```javascript
slide.background = { color: theme.bg };

// 左侧深蓝色带（约 1/3 宽度）
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0, y: 0, w: 3.8, h: 5.625,
  fill: { color: theme.primary }
});
// 天蓝细竖线（色带右边界装饰）
slide.addShape(pres.shapes.RECTANGLE, {
  x: 3.8, y: 0, w: 0.06, h: 5.625,
  fill: { color: theme.accent }
});

// 主标题（白色，左侧色带内）
slide.addText("战略报告标题", {
  x: 0.35, y: 1.4, w: 3.1, h: 1.8,
  fontSize: 28, fontFace: "Microsoft YaHei",
  color: "FFFFFF", bold: true,
  align: "left", valign: "top", margin: 0
});
// 副标题
slide.addText("副标题 · 部门 · 2024", {
  x: 0.35, y: 3.35, w: 3.1, h: 0.4,
  fontSize: 13, fontFace: "Microsoft YaHei",
  color: theme.light, align: "left", margin: 0
});

// 右侧核心信息摘要（可选，1–2 行关键数据）
slide.addText("核心洞察摘要", {
  x: 4.2, y: 2.3, w: 5.4, h: 0.5,
  fontSize: 18, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true, align: "left", margin: 0
});
```

### TOC（目录）

左侧深蓝色带（含"目录"标签）+ 右侧章节列表（蓝色序号圆圈 + 竖线 + 标题 + 描述）。

```javascript
function createTOCSlide(pres, theme, chapters, slideNum) {
  // chapters: [{ num?, title, desc? }]
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧深蓝色带
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 2.2, h: 5.625,
    fill: { color: theme.primary }
  });
  // 天蓝细竖线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 2.2, y: 0, w: 0.06, h: 5.625,
    fill: { color: theme.accent }
  });
  // "目录" 中文标签
  slide.addText("目录", {
    x: 0.15, y: 2.15, w: 1.9, h: 0.65,
    fontSize: 28, fontFace: "Microsoft YaHei", color: theme.headerText,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  slide.addText("AGENDA", {
    x: 0.15, y: 2.85, w: 1.9, h: 0.32,
    fontSize: 11, fontFace: "Arial", color: theme.light,
    align: "center", margin: 0
  });

  // 章节列表
  const startY = 0.65;
  const itemH = Math.min(0.9, 4.2 / Math.max(chapters.length, 1));

  chapters.forEach((ch, i) => {
    const cy = startY + i * itemH;
    const circY = cy + (itemH - 0.42) / 2;

    // 序号圆圈
    slide.addShape(pres.shapes.OVAL, {
      x: 2.55, y: circY, w: 0.42, h: 0.42,
      fill: { color: theme.accent }
    });
    slide.addText(String(ch.num || i + 1).padStart(2, "0"), {
      x: 2.55, y: circY, w: 0.42, h: 0.42,
      fontSize: 12, fontFace: "Arial", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    // 竖线分隔
    slide.addShape(pres.shapes.LINE, {
      x: 3.1, y: cy + itemH * 0.12, w: 0, h: itemH * 0.76,
      line: { color: theme.border, width: 0.75 }
    });
    // 章节标题
    slide.addText(ch.title, {
      x: 3.25, y: cy + (ch.desc ? 0.04 : (itemH - 0.45) / 2), w: 6.3, h: 0.45,
      fontSize: 15, fontFace: "Microsoft YaHei", color: theme.primary,
      bold: true, align: "left", valign: "middle", margin: 0
    });
    // 章节描述（可选）
    if (ch.desc) {
      slide.addText(ch.desc, {
        x: 3.25, y: cy + 0.5, w: 6.3, h: itemH - 0.55,
        fontSize: 10, fontFace: "Microsoft YaHei", color: theme.mutedText,
        align: "left", valign: "top", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
createTOCSlide(pres, theme, [
  { title: "现状诊断",   desc: "市场环境与当前痛点分析" },
  { title: "战略方向",   desc: "三大核心举措与优先级" },
  { title: "实施路径",   desc: "分阶段推进计划与资源配置" },
  { title: "预期成果",   desc: "关键指标与收益估算" },
], 2);
```

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，深蓝背景，白色标题，左侧亮蓝竖条装饰。

### Content（内容页）

背景 `theme.bg`，全宽深蓝标题栏用 `addMcKinseySlideTitle`（Action Title），页码用 `addPageBadge`。

布局选择：

| 内容关系 | 布局 |
|----------|------|
| 并列要点 3–5 条 | `addBulletSection`，蓝色方块前缀 |
| 对比 / 矩阵分析 | 两列或 2×2 卡片，标题栏蓝色 |
| KPI / 核心指标（纯数字） | 横排 2–4 个 `addMcKinseyCard` |
| KPI / 核心指标（带图标） | 横排 2–4 个 `addIconKpiCard`（react-icons） |
| 完成率 / 目标达成 | `makeProgressRing` SVG + 文字说明 |
| 数据汇总 | `addMcKinseyTable` 斑马行表格 |
| 趋势 / 时间序列 | `createFullChartSlide`（LINE 图） |
| 对比分析 + 洞察 | `createChartWithInsightsSlide`（左图右文） |
| 构成 / 占比分析 | `createFullChartSlide`（PIE/DOUGHNUT） |
| 多维评分对比 | `makeHBarChart` SVG |
| 流程 / 实施路径 | `makeProcessNode` SVG 节点 + LINE 连线 |
| 实施路线图 / 里程碑 | `makeTimeline` SVG（跨页底部） |
| 收入 / 成本拆解 | `makeWaterfall` SVG（全宽） |
| 战略分析 (SWOT) | `createSWOTSlide` |
| 多方案 / 竞品对比 | `addComparisonGrid` |
| 多维能力 / 竞争力 | `addMcKinseyRadarChart`（左图）+ 右侧说明 |
| 交叉关系 / 能力交集 | `makeVenn` SVG |

### Summary（总结 / 结尾页）

深蓝背景，白色大字核心结论 + 天蓝分隔线 + 编号行动建议。

```javascript
function createSummarySlide(pres, theme, conclusion, actions, slideNum) {
  // conclusion: string — 一句核心结论
  // actions: [{ text }] — 2–3 条行动建议
  const slide = pres.addSlide();
  slide.background = { color: theme.primary };

  // 顶部天蓝装饰线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.07,
    fill: { color: theme.accent }
  });
  // "核心结论" 标签
  slide.addText("核心结论", {
    x: 0.6, y: 0.45, w: 3, h: 0.32,
    fontSize: 11, fontFace: "Microsoft YaHei", color: theme.light,
    align: "left", margin: 0
  });
  // 大字结论（白色）
  slide.addText(conclusion, {
    x: 0.6, y: 0.82, w: 8.8, h: 1.55,
    fontSize: 26, fontFace: "Microsoft YaHei", color: theme.headerText,
    bold: true, align: "left", valign: "top", margin: 0
  });
  // 分隔线
  slide.addShape(pres.shapes.LINE, {
    x: 0.6, y: 2.55, w: 8.8, h: 0,
    line: { color: theme.accent, width: 1 }
  });
  // "行动建议" 标签
  slide.addText("行动建议", {
    x: 0.6, y: 2.7, w: 3, h: 0.3,
    fontSize: 11, fontFace: "Microsoft YaHei", color: theme.light,
    align: "left", margin: 0
  });
  // 行动条目
  const actionStartY = 3.1;
  const actionH = Math.min(0.58, 1.85 / Math.max(actions.length, 1));
  actions.slice(0, 3).forEach((action, i) => {
    const ay = actionStartY + i * actionH;
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 0.6, y: ay + 0.1, w: 0.28, h: 0.28,
      fill: { color: theme.accent }
    });
    slide.addText(String(i + 1), {
      x: 0.6, y: ay + 0.1, w: 0.28, h: 0.28,
      fontSize: 10, fontFace: "Arial", color: theme.headerText,
      bold: true, align: "center", valign: "middle", margin: 0
    });
    slide.addText(action.text, {
      x: 1.02, y: ay, w: 8.5, h: actionH,
      fontSize: 13, fontFace: "Microsoft YaHei", color: theme.headerText,
      align: "left", valign: "middle", margin: 0
    });
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
// 用法
createSummarySlide(pres, theme,
  "数字化转型三年可降低运营成本 35%，同时提升客户满意度 20 个百分点",
  [
    { text: "Q3 前完成核心系统迁移，确保试点数据采集到位" },
    { text: "成立跨部门数字化工作组，由 COO 直接负责" },
    { text: "2025 年底前完成全量推广，预计 ROI 达 3.2×" },
  ],
  12
);
```

## 麦肯锡风格专项规则

**内容规则：**
- 每张幻灯片有且只有一个中心论点
- Action Title 必须完整传达该论点（读者只看标题也能理解结论）
- 支撑点必须 MECE，避免重叠或遗漏
- 数据必须有来源注释（`addMcKinseySlideTitle` 的 `source` 参数）

**视觉规则：**
- 标题栏必须是深蓝全宽色块（`theme.primary`），不用细线样式
- 禁止使用渐变（背景或形状）
- 卡片边框用细线 `border`，不用纯色填充作强调
- 所有数据表格必须有斑马行，提升可读性
- 禁止纯装饰性图形（所有元素必须承载信息）；但**图表、图标、SVG 进度图均属于信息型视觉元素，应积极使用**
- 每张 Content 页优先选择包含至少一个视觉组件（图表 / 图标卡 / SVG 图形），参考"视觉选择决策树"
