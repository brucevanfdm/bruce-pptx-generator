# Style Preset: Corporate Tech Blue（企业科技蓝）

适合场景：AI / 安全 / 产品 / 解决方案 / 企业级技术类演示，面向国内政企客户的正式商业汇报风格。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深海军蓝 | `1A3C6E` | 标题、主要文字、TOC大数字 |
| `secondary` | 亮蓝 | `1E88E5` | 强调元素、数字、胶囊标签、列头、按钮 |
| `accent` | 橙色 | `F5782A` | **标题下方橙色短横线（标志性元素）**、高亮数字 |
| `light` | 浅蓝 | `E8F4FF` | 卡片背景、浅色填充、斑马行 |
| `bg` | 白 | `FFFFFF` | 内容页背景 |
| `dividerBg` | 极浅蓝 | `EEF6FF` | 章节分隔页背景 |
| `bodyText` | 深灰 | `333333` | 正文段落 |
| `mutedText` | 中灰 | `666666` | 次级文字、说明、描述 |
| `watermark` | 幽灵蓝 | `C8DEFF` | 章节分隔页超大背景数字 |
| `border` | 浅灰蓝 | `D0E4F7` | 卡片边框、分隔线 |

```javascript
const theme = {
  primary:   "1A3C6E",
  secondary: "1E88E5",
  accent:    "F5782A",
  light:     "E8F4FF",
  bg:        "FFFFFF",
  dividerBg: "EEF6FF",
  bodyText:  "333333",
  mutedText: "666666",
  watermark: "C8DEFF",
  border:    "D0E4F7",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 40–48 | Bold | `primary` |
| 封面副标题 | Microsoft YaHei | 18–20 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 28–30 | Bold | `primary` |
| 二级标题 / 卡片标题 | Microsoft YaHei | 16–18 | Bold | `primary` |
| 三级标题 / 特性标题 | Microsoft YaHei | 14–16 | Bold | `primary` |
| 正文 | Microsoft YaHei | 13–14 | Regular | `bodyText` |
| 说明 / 描述 | Microsoft YaHei | 11–12 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 48–64 | Bold | `secondary` 或 `accent` |
| TOC 大数字 | Arial Black | 54 | Bold | `secondary` |
| 章节分隔水印数字 | Arial Black | 200 | Bold | `watermark` |
| 胶囊标签 | Microsoft YaHei | 22–24 | Bold | `FFFFFF` |
| 总结要点 | Microsoft YaHei | 15–16 | Regular | `bodyText` |

## 布局网格系统

幻灯片尺寸 10" × 5.625"。所有元素必须在安全边界内。

**安全边界：**

```
左边界:   x ≥ 0.45"
右边界:   x + w ≤ 9.55"
上边界:   y ≥ 1.05"     （标题区 + accent bar 底部）
下边界:   y + h ≤ 5.0"  （页码徽章 y:5.1，留 0.1" 间距）
内容区高度: 5.0 - 1.05 = 3.95"
内容区宽度: 9.55 - 0.45 = 9.1"
```

**精确列坐标（以 0.45 为左基准，列间距 0.2"）：**

| 布局 | 列1 x | 列1 w | 列2 x | 列2 w | 列3 x | 列3 w | 列4 x | 列4 w |
|------|--------|--------|--------|--------|--------|--------|--------|--------|
| 1列全宽 | 0.45 | 9.1 | — | — | — | — | — | — |
| 2列均等 | 0.45 | 4.45 | 5.1 | 4.45 | — | — | — | — |
| 2列 4:6 | 0.45 | 3.44 | 4.09 | 5.46 | — | — | — | — |
| 2列 6:4 | 0.45 | 5.46 | 6.11 | 3.44 | — | — | — | — |
| 3列均等 | 0.45 | 2.87 | 3.52 | 2.87 | 6.59 | 2.96 | — | — |
| 4列均等 | 0.45 | 2.07 | 2.72 | 2.07 | 4.99 | 2.07 | 7.26 | 2.29 |

**垂直节奏（内容区从 y:1.05 开始）：**

| 条目数 | 起始 y | 行高（含间距） | 最后一行底边 |
|--------|--------|----------------|-------------|
| 3行大内容 | 1.1 | 1.3 | ≤ 5.0 |
| 4行中内容 | 1.1 | 0.97 | ≤ 5.0 |
| 5行小内容 | 1.1 | 0.77 | ≤ 5.0 |
| KPI 4卡片 | 1.25 | — | 卡片 h:3.2，底 4.45 |

**内容密度上限（商业PPT黄金法则）：**

- 每张内容页：正文条目 ≤ 5 条，每条描述 ≤ 2 行
- 每张对比页：列数 ≤ 4，行数 ≤ 6
- 每张 KPI 页：指标数 ≤ 4（2×2 或 4×1）
- 纯文字段落页：字数 ≤ 120 字，段落 ≤ 3 段
- 不允许在同一区域同时出现 4 种以上颜色

## 标志性设计元素

### 1. 标题 + 橙色下划线（所有非封面页必用）

橙色短横条是本风格最核心的标识，每张非封面幻灯片标题下方必须有。

```javascript
function addSlideTitleWithAccent(slide, pres, theme, title) {
  slide.addText(title, {
    x: 0.45, y: 0.22, w: 9.1, h: 0.52,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 橙色短横线：固定宽度 0.4"，与标题左对齐
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.80, w: 0.4, h: 0.06,
    fill: { color: theme.accent }
  });
  // 标题区右侧可选：灰色细线延伸至右边界（增强秩序感）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.95, y: 0.82, w: 8.6, h: 0.01,
    fill: { color: theme.border }
  });
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
    fontSize: 12, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. 章节分隔页：水印大数字 + 胶囊标签

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 超大水印数字（装饰性背景层）
  slide.addText(String(num).padStart(2, '0'), {
    x: 0, y: 0.2, w: 6.5, h: 5.2,
    fontSize: 200, fontFace: "Arial Black",
    color: theme.watermark, bold: true, align: "left", margin: 0
  });

  // 胶囊标签背景
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fill: { color: theme.secondary },
    rectRadius: 0.34
  });
  // 胶囊标签文字
  slide.addText(title, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fontSize: 22, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
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

大数字 + 竖线分隔 + 标题 + 副标题。`x` 参数决定条目起始位置，`maxW` 限制右侧文字宽度。

```javascript
function addTOCItem(slide, pres, theme, x, y, num, title, subtitle, maxW) {
  // maxW: 条目总宽度（文字区 = maxW - 1.05）
  const textX = x + 1.05;
  const textW = (maxW !== undefined) ? (x + maxW - textX) : (9.55 - textX);

  // 大数字
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: 0.85, h: 0.65,
    fontSize: 54, fontFace: "Arial Black",
    color: theme.secondary, bold: true, align: "right", valign: "middle", margin: 0
  });
  // 竖分隔线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x + 0.9, y: y + 0.09, w: 0.04, h: 0.5,
    fill: { color: theme.secondary }
  });
  // 标题
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.36,
    fontSize: 17, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "bottom", margin: 0
  });
  // 副标题
  slide.addText(subtitle, {
    x: textX, y: y + 0.35, w: textW, h: 0.28,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", valign: "top", margin: 0
  });
}

// 目录页用法示例（5个条目，x:4.8 开始，条目宽度 4.75"，行距 0.73"）：
// addTOCItem(slide, pres, theme, 4.8, 0.62, 1, "产品背景", "现状威胁、标准规范", 4.75);
// addTOCItem(slide, pres, theme, 4.8, 1.35, 2, "产品介绍", "产品概述、4大核心功能", 4.75);
// addTOCItem(slide, pres, theme, 4.8, 2.08, 3, "部署成效", "产品选型、产品部署、产品成效", 4.75);
// addTOCItem(slide, pres, theme, 4.8, 2.81, 4, "产品亮点", "核心技术、特色功能", 4.75);
// addTOCItem(slide, pres, theme, 4.8, 3.54, 5, "案例资质", "实战案例、合作客户", 4.75);
```

### 5. 特性条目（Feature Item）

用于功能特性列表页。**必须显式传入 `zoneW`（所在区域宽度），避免文字溢出分区边界。**

```javascript
function addFeatureItem(slide, pres, theme, x, y, num, title, description, zoneW) {
  // zoneW: 该条目所在列的宽度（如右半区 zoneW = 4.45）
  const circleSize = 0.44;
  const gap = 0.14;        // 圆圈右侧到文字左侧的间距
  const textX = x + circleSize + gap;
  const textW = zoneW - circleSize - gap;

  // 蓝色圆形背景
  slide.addShape(pres.shapes.OVAL, {
    x: x, y: y + 0.01, w: circleSize, h: circleSize,
    fill: { color: theme.secondary }
  });
  // 圆圈内数字
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y + 0.01, w: circleSize, h: circleSize,
    fontSize: 13, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // 特性标题（与圆圈垂直居中对齐）
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.32,
    fontSize: 15, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 特性描述（限 2 行）
  slide.addText(description, {
    x: textX, y: y + 0.34, w: textW, h: 0.54,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", valign: "top", margin: 0
  });
}

// 4个特性，右半区（x:5.1, zoneW:4.45），y 间距 0.97"：
// addFeatureItem(slide, pres, theme, 5.1, 1.1,  1, "多维风险分析", "通过实时风险指标大盘...", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 2.07, 2, "事件确认管理", "提供完整的事件处置流程...", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 3.04, 3, "调用记录审计", "管理并提供所有调用记录...", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 4.01, 4, "操作行为追溯", "完整记录平台管理员操作...", 4.45);
// 注：第4条 y:4.01 + 0.34 + 0.54 = 4.89 ≤ 5.0，安全
```

### 6. KPI 指标卡（4 宫格）

用于成效数据页、关键指标展示页。

```javascript
function addKPICard(slide, pres, theme, x, y, w, h, value, unit, label, color) {
  // color: theme.secondary 或 theme.accent（主数字颜色）
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: h,
    fill: { color: theme.light },
    line: { color: theme.border, width: 1 }
  });
  // 顶部强调色细条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.06,
    fill: { color: color || theme.secondary }
  });
  // 大数字
  slide.addText(value, {
    x: x, y: y + 0.25, w: w, h: 1.0,
    fontSize: 56, fontFace: "Arial Black",
    color: color || theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 单位（叠加在大数字右侧区域）
  if (unit) {
    slide.addText(unit, {
      x: x, y: y + 0.9, w: w, h: 0.38,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: color || theme.secondary, bold: true,
      align: "center", margin: 0
    });
  }
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + h - 0.42, w: w - 0.2, h: 0.38,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });
}

// 4 宫格用法（2×2，列间距 0.2"）：
// const kW = 4.45, kH = 1.7, kGap = 0.2;
// addKPICard(slide, pres, theme, 0.45,        1.25, kW, kH, "99.9", "%",  "系统可用率", theme.secondary);
// addKPICard(slide, pres, theme, 0.45 + kW + kGap, 1.25, kW, kH, "2.4", "亿+", "数据处理量",  theme.accent);
// addKPICard(slide, pres, theme, 0.45,        1.25 + kH + kGap, kW, kH, "300", "ms", "平均响应时间", theme.secondary);
// addKPICard(slide, pres, theme, 0.45 + kW + kGap, 1.25 + kH + kGap, kW, kH, "50+", "家", "标杆客户",  theme.accent);
```

### 7. 流程步骤条（Process Step）

用于实施路径、解决方案步骤页，横向排列。

```javascript
function addProcessStep(slide, pres, theme, x, y, w, stepNum, totalSteps, title, desc) {
  // 步骤圆圈
  const circleSize = 0.5;
  const centerX = x + w / 2;

  // 连接线（非最后一步，画到右侧下一步）
  if (stepNum < totalSteps) {
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + w, y: y + circleSize / 2 - 0.01, w: (w * 0.3) /* 由调用者控制 gap */, h: 0.02,
      fill: { color: theme.border }
    });
  }

  // 圆圈背景
  slide.addShape(pres.shapes.OVAL, {
    x: centerX - circleSize / 2, y: y, w: circleSize, h: circleSize,
    fill: { color: stepNum === 1 ? theme.accent : theme.secondary }
  });
  // 步骤数字
  slide.addText(String(stepNum), {
    x: centerX - circleSize / 2, y: y, w: circleSize, h: circleSize,
    fontSize: 18, fontFace: "Arial Black", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // 标题
  slide.addText(title, {
    x: x, y: y + 0.58, w: w, h: 0.36,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "center", margin: 0
  });
  // 描述
  slide.addText(desc, {
    x: x, y: y + 0.96, w: w, h: 0.7,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "center", margin: 0
  });
}

// 4步流程，均匀分布在内容区（每列 w:2.07，列间距 0.2"）：
// addProcessStep(slide, pres, theme, 0.45, 1.5, 2.07, 1, 4, "需求调研", "梳理业务场景\n识别核心诉求");
// addProcessStep(slide, pres, theme, 2.72, 1.5, 2.07, 2, 4, "方案设计", "架构规划\n模块定义");
// addProcessStep(slide, pres, theme, 4.99, 1.5, 2.07, 3, 4, "部署实施", "环境配置\n系统集成");
// addProcessStep(slide, pres, theme, 7.26, 1.5, 2.07, 4, 4, "运营交付", "验收测试\n持续优化");
```

### 8. 蓝色列头（Column Header）

用于对比页、能力清单列页。

```javascript
function addColumnHeader(slide, pres, theme, x, y, w, text) {
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.42,
    fill: { color: theme.secondary }
  });
  slide.addText(text, {
    x: x, y: y, w: w, h: 0.42,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 9. 信息卡片（Info Card）

用于案例页、痛点卡、解决方案模块。

`bodyLines` 可以是字符串（单段）或 PptxGenJS 富文本数组（多行/混合格式）。
最小高度 `h ≥ 0.8`（条头 0.36 + 内边距 0.1 + 内容最小 0.34）。

```javascript
function addInfoCard(slide, pres, theme, x, y, w, h, headerText, bodyLines) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: h,
    fill: { color: theme.light },
    line: { color: theme.border, width: 1 }
  });
  // 蓝色条头
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.36,
    fill: { color: theme.secondary }
  });
  // 条头文字
  slide.addText(headerText, {
    x: x + 0.12, y: y, w: w - 0.14, h: 0.36,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "left", valign: "middle", margin: 0
  });
  // 卡片内容（内边距 0.14"）
  slide.addText(bodyLines, {
    x: x + 0.14, y: y + 0.44, w: w - 0.28, h: h - 0.55,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", valign: "top", margin: 0
  });
}
```

## 装饰元素库

两种使用模式：**背景纹理**（高透明度，`transparency ≥ 85`，不抢夺注意力）；**封面图形**（中透明度，`transparency 55–75`，作为构成元素）。

所有装饰元素必须放在内容元素**之前**添加，确保内容层叠在装饰层上方。

### D1. 点阵背景

最克制的纹理。适合：内容页右上角、封面留白区、章节分隔页。

```javascript
/**
 * @param {number} x/y/w/h - 点阵覆盖区域
 * @param {object} opts
 *   spacing     - 点间距，默认 0.38"
 *   dotSize     - 点直径，默认 0.07"
 *   color       - 颜色，默认 theme.secondary
 *   transparency - 0-100，默认 88（背景模式）/ 65（封面模式）
 */
function addBgDotGrid(slide, pres, theme, x, y, w, h, opts = {}) {
  const spacing     = opts.spacing      ?? 0.38;
  const dotSize     = opts.dotSize      ?? 0.07;
  const color       = opts.color        ?? theme.secondary;
  const transp      = opts.transparency ?? 88;

  const cols = Math.ceil(w / spacing);
  const rows = Math.ceil(h / spacing);

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      const dx = x + c * spacing;
      const dy = y + r * spacing;
      if (dx + dotSize > x + w || dy + dotSize > y + h) continue;
      slide.addShape(pres.shapes.OVAL, {
        x: dx, y: dy, w: dotSize, h: dotSize,
        fill: { color: color, transparency: transp }
      });
    }
  }
}

// 用法示例：
// 内容页右上角点阵（背景模式）
// addBgDotGrid(slide, pres, theme, 7.0, 0.9, 2.55, 1.8, { transparency: 88 });
//
// 封面右区点阵（封面模式，略深）
// addBgDotGrid(slide, pres, theme, 6.1, 0.1, 3.9, 5.5, { spacing: 0.42, transparency: 78 });
```

### D2. 同心圆环

有层次感的几何装饰。适合：封面右区、感谢页背景。仅使用描边（无填充），自然产生透视感。

```javascript
/**
 * @param {number} cx/cy - 圆心坐标
 * @param {object} opts
 *   rings  - [{ r, transparency }] 半径和透明度数组
 *   color  - 默认 theme.secondary
 *   lineWidth - 描边宽度，默认 1.0pt
 */
function addCircleRings(slide, pres, theme, cx, cy, opts = {}) {
  const color     = opts.color     ?? theme.secondary;
  const lineWidth = opts.lineWidth ?? 1.0;
  const rings     = opts.rings ?? [
    { r: 0.9,  transparency: 60 },
    { r: 1.5,  transparency: 70 },
    { r: 2.1,  transparency: 78 },
    { r: 2.7,  transparency: 85 },
  ];

  rings.forEach(({ r, transparency }) => {
    slide.addShape(pres.shapes.OVAL, {
      x: cx - r, y: cy - r, w: r * 2, h: r * 2,
      fill: { type: "none" },
      line: { color: color, width: lineWidth, transparency: transparency }
    });
  });
}

// 封面右区用法（圆心在右区中部）：
// addCircleRings(slide, pres, theme, 8.05, 2.8, {
//   rings: [
//     { r: 0.8,  transparency: 55 },
//     { r: 1.4,  transparency: 65 },
//     { r: 2.0,  transparency: 75 },
//     { r: 2.6,  transparency: 85 },
//   ]
// });
//
// 感谢页水印圆环（更大、更透明）：
// addCircleRings(slide, pres, theme, 5.0, 2.8, {
//   rings: [
//     { r: 1.2, transparency: 75 },
//     { r: 2.0, transparency: 82 },
//     { r: 2.8, transparency: 88 },
//   ],
//   color: theme.primary
// });
```

### D3. 几何角落装饰

两个旋转矩形叠加，产生立体感角落。适合：封面、感谢页、章节分隔页。

```javascript
/**
 * @param {"TR"|"BR"|"BL"|"TL"} corner - 目标角落
 * @param {object} opts
 *   size        - 基础尺寸，默认 1.4"
 *   color1      - 大矩形颜色，默认 theme.primary
 *   color2      - 小矩形颜色，默认 theme.secondary
 *   transparency - 基础透明度，默认 80（背景模式 88）
 */
function addCornerGeometry(slide, pres, theme, corner, opts = {}) {
  const size   = opts.size        ?? 1.4;
  const c1     = opts.color1      ?? theme.primary;
  const c2     = opts.color2      ?? theme.secondary;
  const transp = opts.transparency ?? 80;

  const positions = {
    TR: { x: 10 - size * 1.1, y: -size * 0.2 },
    BR: { x: 10 - size * 1.0, y: 5.625 - size * 0.9 },
    BL: { x: -size * 0.2,     y: 5.625 - size * 1.0 },
    TL: { x: -size * 0.2,     y: -size * 0.2 },
  };
  const { x, y } = positions[corner];
  const rot = { TR: 20, BR: 65, BL: 20, TL: 65 };

  // 大矩形
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: x, y: y, w: size, h: size,
    rectRadius: 0.12,
    fill: { color: c1, transparency: transp },
    rotate: rot[corner]
  });
  // 错位小矩形
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: x + size * 0.28, y: y + size * 0.28,
    w: size * 0.72, h: size * 0.72,
    rectRadius: 0.1,
    fill: { color: c2, transparency: transp + 8 },
    rotate: rot[corner] + 18
  });
}

// 封面右上角 + 左下角组合：
// addCornerGeometry(slide, pres, theme, "TR", { size: 1.6, transparency: 78 });
// addCornerGeometry(slide, pres, theme, "BL", { size: 1.0, transparency: 85 });
```

### D4. 斜线条纹

最轻盈的纹理，几乎不影响可读性。适合：内容页全版背景纹理、封面留白区。

```javascript
/**
 * @param {number} x/y/w/h - 条纹覆盖区域
 * @param {object} opts
 *   spacing     - 条纹间距，默认 0.5"
 *   color       - 默认 theme.secondary
 *   transparency - 默认 92（极克制）
 *   lineWidth   - 默认 0.5pt
 */
function addDiagonalStripes(slide, pres, theme, x, y, w, h, opts = {}) {
  const spacing = opts.spacing      ?? 0.5;
  const color   = opts.color        ?? theme.secondary;
  const transp  = opts.transparency ?? 92;
  const lw      = opts.lineWidth    ?? 0.5;

  // LINE shape: (x,y) → (x+w, y+h)，利用 w/h 同值实现 45° 对角
  const count = Math.ceil((w + h) / spacing) + 1;
  for (let i = 0; i < count; i++) {
    const offset = i * spacing - h;  // 让线条从区域左上扫到右下
    // 计算裁剪后的线段起止点
    let lx1 = x + offset;
    let ly1 = y;
    let lx2 = x + offset + h;
    let ly2 = y + h;

    // 裁剪到区域内
    if (lx1 < x) { ly1 += (x - lx1); lx1 = x; }
    if (lx2 > x + w) { ly2 -= (lx2 - (x + w)); lx2 = x + w; }
    if (lx1 >= lx2 || ly1 >= ly2) continue;

    slide.addShape(pres.shapes.LINE, {
      x: lx1, y: ly1,
      w: lx2 - lx1, h: ly2 - ly1,
      line: { color: color, width: lw, transparency: transp }
    });
  }
}

// 内容页右半区轻纹理：
// addDiagonalStripes(slide, pres, theme, 5.1, 1.0, 4.45, 4.0, { transparency: 93 });
//
// 封面右区轻纹理（叠在浅蓝背景上）：
// addDiagonalStripes(slide, pres, theme, 6.1, 0.1, 3.9, 5.5, { spacing: 0.4, transparency: 90 });
```

### 装饰元素组合规则

| 使用场景 | 推荐组合 | 透明度范围 |
|----------|----------|------------|
| 内容页背景（极克制） | 点阵 D1 放在一个角落 | 88–93 |
| 章节分隔页 | 点阵 D1 + 圆环 D2（右侧） | 80–88 |
| 封面右区 | 圆环 D2 + 角落几何 D3 + 斜线 D4 | 65–82 |
| 感谢页 | 圆环 D2（全页，大半径） | 75–88 |
| **禁止** | 同一页面超过 2 种装饰类型 | — |
| **禁止** | 装饰元素叠加在正文文字区域 | — |

## 各页类型布局

### 封面页（Cover）

**变体 A：左文右图（推荐，适合有产品视觉素材时）**

设计原则：大区域保持浅色，深色仅用于细条和文字。右区用圆环 + 斜线纹理构建视觉层次（装饰层 → 结构层 → 内容层，顺序不可颠倒）。

```
| [顶部深蓝细条]                                         |
| 主标题（大，左对齐）   | [浅蓝右区]                    |
| 橙色短横线             | [斜线纹理 D4，极克制]         |
| 副标题                 | [同心圆环 D2，中透明度]       |
| 日期 / 场合            | [角落几何 D3，右下]           |
|                        | 公司名（深色文字，底部）      |
| [底部亮蓝细条]                                         |
```

```javascript
function createCoverSlide(pres, theme, title, subtitle, dateOrEvent, company) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // ── 层 1：结构色块（最底层）──────────────────────────
  // 顶部深蓝细条（品牌标识）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.1,
    fill: { color: theme.primary }
  });
  // 右区浅蓝背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 6.05, y: 0.1, w: 3.95, h: 5.525,
    fill: { color: theme.light }
  });
  // 左右分区竖线（亮蓝细条）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 6.0, y: 0, w: 0.06, h: 5.625,
    fill: { color: theme.secondary }
  });
  // 底部亮蓝细条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 5.52, w: 10, h: 0.1,
    fill: { color: theme.secondary }
  });

  // ── 层 2：装饰纹理（叠在背景上，内容之下）──────────
  // 右区斜线纹理（极克制）
  addDiagonalStripes(slide, pres, theme, 6.1, 0.1, 3.9, 5.5, {
    spacing: 0.42, transparency: 91
  });
  // 右区同心圆环（圆心在右区中偏上，作为视觉焦点）
  addCircleRings(slide, pres, theme, 8.05, 2.5, {
    rings: [
      { r: 0.7,  transparency: 58 },
      { r: 1.2,  transparency: 68 },
      { r: 1.75, transparency: 76 },
      { r: 2.3,  transparency: 84 },
    ]
  });
  // 右下角几何装饰
  addCornerGeometry(slide, pres, theme, "BR", {
    size: 1.1, transparency: 80,
    color1: theme.primary, color2: theme.secondary
  });

  // ── 层 3：内容文字（最顶层）────────────────────────
  // 主标题
  slide.addText(title, {
    x: 0.45, y: 1.2, w: 5.3, h: 1.8,
    fontSize: 42, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left",
    fit: "shrink", margin: 0
  });
  // 橙色短横线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 3.18, w: 0.5, h: 0.07,
    fill: { color: theme.accent }
  });
  // 副标题
  slide.addText(subtitle, {
    x: 0.45, y: 3.32, w: 5.3, h: 0.45,
    fontSize: 18, fontFace: "Microsoft YaHei",
    color: theme.secondary, align: "left", margin: 0
  });
  // 日期/场合
  if (dateOrEvent) {
    slide.addText(dateOrEvent, {
      x: 0.45, y: 3.88, w: 5.3, h: 0.32,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }
  // 右区：公司名（深色文字，浅蓝背景上）
  if (company) {
    slide.addText(company, {
      x: 6.15, y: 4.85, w: 3.7, h: 0.38,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true, align: "center", margin: 0
    });
  }

  return slide;
}
```

**变体 B：居中简约（适合演讲开场，无需复杂视觉素材）**

```
| [顶部深蓝色全宽横幅，含公司名]          |
|                                          |
|         主标题（居中，大）               |
|         橙色短横线（居中）               |
|         副标题（居中）                   |
|                                          |
| [底部信息栏：日期 / 部门 / 场合]         |
```

```javascript
function createCoverSlideCentered(pres, theme, title, subtitle, dateOrEvent, company) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 顶部深蓝细条 + 亮蓝细条（双线品牌标识，替代大色块横幅）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.1,
    fill: { color: theme.primary }
  });
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0.1, w: 10, h: 0.05,
    fill: { color: theme.secondary }
  });
  // 公司名（白底上深色文字）
  if (company) {
    slide.addText(company, {
      x: 0.5, y: 0.2, w: 9, h: 0.55,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true, align: "center", valign: "middle", margin: 0
    });
  }

  // 主标题
  slide.addText(title, {
    x: 0.5, y: 1.5, w: 9, h: 1.6,
    fontSize: 46, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "center",
    fit: "shrink", margin: 0
  });
  // 橙色短横线（居中：x = 5 - 0.4）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 4.6, y: 3.22, w: 0.8, h: 0.07,
    fill: { color: theme.accent }
  });
  // 副标题
  slide.addText(subtitle, {
    x: 0.5, y: 3.36, w: 9, h: 0.42,
    fontSize: 20, fontFace: "Microsoft YaHei",
    color: theme.secondary, align: "center", margin: 0
  });

  // 底部信息栏（浅蓝底，非深色）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 4.95, w: 10, h: 0.675,
    fill: { color: theme.light }
  });
  // 底部信息栏顶部细线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 4.95, w: 10, h: 0.04,
    fill: { color: theme.border }
  });
  if (dateOrEvent) {
    slide.addText(dateOrEvent, {
      x: 0.5, y: 4.95, w: 9, h: 0.675,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "center", valign: "middle", margin: 0
    });
  }

  return slide;
}
```

### 目录页（TOC）

```
| [左半区：3D图标或装饰图]  | 目录 CONTENTS           |
|                           | 01 | 产品背景  现状威胁… |
|                           | 02 | 产品介绍  产品概述… |
|                           | 03 | 部署成效  产品选型… |
|                           | 04 | 产品亮点  核心技术… |
|                           | 05 | 案例资质  实战案例… |
```

- 背景白色 `theme.bg`
- 左侧 3D 图标图片：`x:0.3, y:0.8, w:4.0, h:4.0`；无图时用蓝色装饰块替代
- 顶左："目录" 28pt bold `primary`；下方 "CONTENTS" 14pt `watermark` 色装饰字
- 右侧 5 个条目用 `addTOCItem()`，`x:4.8, maxW:4.75`，起始 `y:0.62`，行距 `0.73"`
- 页码徽章用 `addPageBadge()`

### 章节分隔页（Section Divider）

用 `createSectionDividerSlide()` 生成，所有分隔页保持视觉一致。
- 背景 `theme.dividerBg`（`EEF6FF`），不可使用其他背景色
- 水印数字从 `x:0` 起，字体极大时视觉上超出左边界是正常效果

### 内容页（Content）

所有内容页必须遵守：
- 背景 `theme.bg`（`FFFFFF`），全部内容页使用同一背景值
- 标题用 `addSlideTitleWithAccent()`，标题 + accent bar 整体占 `y:0.22–0.88`
- 内容区从 `y:1.05` 开始，不超过 `y:5.0`
- 页码徽章用 `addPageBadge()`

**子类型选择：**

| 子类型 | 布局 | 典型用途 |
|--------|------|----------|
| 特性列表 | 左半 3D 图标 + 右半 `addFeatureItem()×4` | 功能模块详解 |
| KPI 指标 | 2×2 `addKPICard()` | 成效数据、关键指标 |
| 流程步骤 | 4×1 `addProcessStep()` | 实施路径、方法论 |
| 痛点分析 | 3 列 `addInfoCard()` | 客户痛点、挑战场景 |
| 对比矩阵 | `addColumnHeader()` + 行列数据 | 能力对比、方案选型 |
| 架构示意 | 分层矩形 + 连接线 | 产品架构、系统集成 |
| 文字分析 | 正文段落 + 底部双卡片 | 背景现状、政策解读 |
| 数据大字 | 大字号数据 (56–72pt) + 说明 | 单指标突出展示 |

**痛点分析页（3列卡片）布局示例：**

```javascript
// 3 列均等卡片（w:2.87，间距 0.2"），高度 h:2.8
// addInfoCard(slide, pres, theme, 0.45, 1.15, 2.87, 2.8, "痛点一：数据孤岛", "各系统数据分散...");
// addInfoCard(slide, pres, theme, 3.52, 1.15, 2.87, 2.8, "痛点二：响应滞后", "告警处理依赖人工...");
// addInfoCard(slide, pres, theme, 6.59, 1.15, 2.96, 2.8, "痛点三：合规压力", "等保 2.0 要求...");
```

### 案例页（Case Study）

```
| 标题：应用案例——XX单位AI安全防护         |
| [橙色短横线]                             |
| [项目背景卡片 w:4.45]  | [核心痛点卡片 w:4.45] |
|                                          |
| [客户收获：3列图标 + 文字]               |
```

- 上半双卡片：`addInfoCard()`，`w:4.45, h:2.1`，左 `x:0.45`，右 `x:5.1`，`y:1.05`
- 下方收获区：3列（w:2.87），每列含圆形图标 + 标题 + 描述，`y:3.35`
- 页码徽章用 `addPageBadge()`

### 总结/收尾页（Summary / Closing）

**变体 A：核心要点回顾（适合数据/产品汇报）**

```
| 标题：核心亮点   [橙色短横线]           |
|                                         |
|  ① 要点标题  ——————————————————————    |
|     要点描述文字                        |
|  ② 要点标题  ——————————————————————    |
|     要点描述文字                        |
|  ③ 要点标题  ——————————————————————    |
```

```javascript
function createSummarySlide(pres, theme, slideNum, points) {
  // points: [{ num, title, desc }]，建议 3–4 条
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addSlideTitleWithAccent(slide, pres, theme, "核心亮点");

  const startY = 1.1;
  const itemH = (4.9 - startY) / points.length;  // 均匀分配高度

  points.forEach(({ num, title, desc }, i) => {
    const y = startY + i * itemH;
    // 数字圆圈
    slide.addShape(pres.shapes.OVAL, {
      x: 0.45, y: y + 0.06, w: 0.38, h: 0.38,
      fill: { color: theme.secondary }
    });
    slide.addText(String(num).padStart(2, '0'), {
      x: 0.45, y: y + 0.06, w: 0.38, h: 0.38,
      fontSize: 12, fontFace: "Arial", color: "FFFFFF",
      bold: true, align: "center", valign: "middle", margin: 0
    });
    // 分隔线
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 1.0, y: y + 0.24, w: 8.55, h: 0.02,
      fill: { color: theme.light }
    });
    // 标题
    slide.addText(title, {
      x: 1.05, y: y, w: 8.5, h: 0.32,
      fontSize: 15, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true, align: "left", margin: 0
    });
    // 描述（若无描述，itemH 内无需预留空间）
    if (desc) {
      slide.addText(desc, {
        x: 1.05, y: y + 0.34, w: 8.5, h: itemH - 0.42,
        fontSize: 12, fontFace: "Microsoft YaHei",
        color: theme.bodyText, align: "left", margin: 0
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

**变体 B：下一步行动（适合项目提案、销售汇报）**

```
| 标题：下一步行动  [橙色短横线]          |
|                                         |
|  [阶段1卡片]  [阶段2卡片]  [阶段3卡片] |
|                                         |
|  联系方式：xxx@company.com              |
```

三列卡片：`addInfoCard()`，`w:2.87`，`x` 分别为 `0.45 / 3.52 / 6.59`，`y:1.15, h:3.0`。
底部联系信息行：`y:4.55, h:0.38, fontSize:13, color: mutedText, align: center`。

**变体 C：感谢/Q&A（适合演讲收尾）**

设计原则：白底居中，顶底细条收边，水印装饰字作背景层。

```
| [顶部深蓝细条]                        |
|   [超大浅蓝水印字"Q&A"，装饰背景层]   |
|         感谢聆听（居中，粗体）         |
|         橙色短横线（居中）             |
|         副语（居中，可选）             |
|         联系方式（居中）               |
| [底部亮蓝细条]                        |
```

```javascript
function createThankYouSlide(pres, theme, slideNum, contactInfo, subtitle) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 顶部深蓝细条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 0.1,
    fill: { color: theme.primary }
  });
  // 底部亮蓝细条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 5.52, w: 10, h: 0.1,
    fill: { color: theme.secondary }
  });

  // 装饰层：全页大圆环（背景层，与内容不重叠）
  addCircleRings(slide, pres, theme, 5.0, 2.8, {
    rings: [
      { r: 1.0, transparency: 72 },
      { r: 1.7, transparency: 80 },
      { r: 2.4, transparency: 87 },
    ],
    color: theme.primary,
    lineWidth: 1.5
  });
  // 左侧点阵（只放左半区，不遮挡中部文字）
  addBgDotGrid(slide, pres, theme, 0.3, 0.5, 2.5, 4.5, { transparency: 90 });

  // 感谢文字（居中）
  slide.addText("感谢聆听", {
    x: 1.0, y: 1.4, w: 8.0, h: 1.0,
    fontSize: 46, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "center", margin: 0
  });
  // 橙色短横线（居中）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 4.6, y: 2.55, w: 0.8, h: 0.07,
    fill: { color: theme.accent }
  });
  // 副语
  if (subtitle) {
    slide.addText(subtitle, {
      x: 1.0, y: 2.72, w: 8.0, h: 0.4,
      fontSize: 15, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "center", margin: 0
    });
  }
  // 联系方式
  if (contactInfo) {
    slide.addText(contactInfo, {
      x: 1.0, y: 3.3, w: 8.0, h: 0.35,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "center", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

## 注意事项

**对齐与秩序**
- **橙色下划线是本风格最重要的标识**，所有非封面幻灯片标题下方不可省略
- 内容区左边界统一 `x:0.45`，右边界统一 `x+w ≤ 9.55`，所有元素必须在此范围内
- 多列布局必须使用"布局网格系统"中的精确 x 坐标，不允许凭感觉调整列间距
- 同一页面内相同层级的元素，`fontSize` 和 `color` 必须完全一致

**函数使用**
- `addFeatureItem` 必须显式传入 `zoneW` 参数（所在列宽度），不可依赖默认推断
- `addTOCItem` 必须显式传入 `maxW` 参数，避免右侧条目文字溢出幻灯片
- `addInfoCard` 内容框已预留 0.14" 内边距，`bodyLines` 文字不需额外缩进

**背景色**
- **内容页背景统一用 `theme.bg`**（`FFFFFF`），compile.js 中定义一次，确保所有内容页值相同
- **分隔页背景统一用 `theme.dividerBg`**（`EEF6FF`），不要在函数内硬编码颜色字符串

**字体**
- 所有中文使用 `Microsoft YaHei`，大数字（TOC、水印、KPI）使用 `Arial Black`
- 正文字号不低于 12pt，说明文字不低于 11pt

**形状边框**
- 不需要边框时直接省略 `line` 属性
- 若需明确关闭边框，使用 `line: { color: theme.bg, width: 0 }`

**水印数字**
- 水印数字从 `x:0` 起，字体极大时会视觉上超出左边界，这是正常渲染效果，无需修正
