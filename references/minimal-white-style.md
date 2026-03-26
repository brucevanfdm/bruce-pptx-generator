# Style Preset: Minimal White（简约白）

适合场景：内部报告、数据汇报、投资人 Deck、快速同步会议。追求克制、专业、不分散注意力的视觉风格。

## 氛围

**简洁高效** — 大量留白、极简线条、内容本身即设计。让数据和结论成为主角，装饰退到底层。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 炭黑 | `1A1A1A` | 标题、主要文字 |
| `secondary` | 深灰 | `4A4A4A` | 副标题、次级文字、数字 |
| `accent` | 草绿 | `2D7D46` | 标题下方细线、关键数字、CTA |
| `light` | 极浅灰 | `F5F5F5` | 卡片背景、斑马行 |
| `bg` | 纯白 | `FFFFFF` | 所有内容页背景 |
| `dividerBg` | 浅灰 | `F0F0F0` | 章节分隔页背景 |
| `bodyText` | 深灰 | `333333` | 正文段落 |
| `mutedText` | 中灰 | `888888` | 次级文字、说明、描述 |
| `watermark` | 浅灰 | `E0E0E0` | 章节分隔页水印数字 |
| `border` | 浅灰线 | `DDDDDD` | 卡片边框、分隔线 |

```javascript
const theme = {
  primary:   "1A1A1A",
  secondary: "4A4A4A",
  accent:    "2D7D46",
  light:     "F5F5F5",
  bg:        "FFFFFF",
  dividerBg: "F0F0F0",
  bodyText:  "333333",
  mutedText: "888888",
  watermark: "E0E0E0",
  border:    "DDDDDD",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 36–44 | Bold | `primary` |
| 封面副标题 | Microsoft YaHei | 16–18 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 24–28 | Bold | `primary` |
| 二级标题 / 卡片标题 | Microsoft YaHei | 15–17 | Bold | `primary` |
| 三级标题 / 特性标题 | Microsoft YaHei | 13–15 | Bold | `secondary` |
| 正文 | Microsoft YaHei | 12–13 | Regular | `bodyText` |
| 说明 / 描述 | Microsoft YaHei | 11–12 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 44–56 | Bold | `accent` 或 `primary` |
| TOC 大数字 | Arial Black | 36 | Bold | `accent` |
| 章节分隔水印数字 | Arial Black | 200 | Bold | `watermark` |

> 简约风避免粗体滥用：卡片描述、正文、说明文字一律 Regular，只有标题和关键数字用 Bold。

## 布局网格系统

幻灯片尺寸 10" × 5.625"，安全边界与企业科技蓝相同。

**简约风特有间距规范：**

- 元素之间间距比企业科技蓝宽 20%（宁可留白，不要拥挤）
- 卡片边框：细线 `border` 颜色，不用色块背景作强调
- 标题字号比企业科技蓝小 2pt（内容更重要）

**内容密度指引（精简汇报型）：**

> 本风格定位为**精简汇报型**，每张幻灯片一个核心结论，辅以最必要的支撑数据。

- 每张内容页：核心条目 3–5 条，每条 1–2 行
- KPI 页：2–4 个指标，不加多余说明，数字说话
- 段落页：最多 2 段，每段 2–3 句
- 标题必须是结论句，不是描述句（如"检测率提升 40%"而非"检测效果"）

## 标志性设计元素

### 1. 标题 + 草绿细线（所有非封面页必用）

本风格标志：极细草绿线，无右侧延伸（保持极简）。

```javascript
function addSlideTitleWithAccent(slide, pres, theme, title) {
  slide.addText(title, {
    x: 0.45, y: 0.22, w: 9.1, h: 0.52,
    fontSize: 26, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 草绿细横线（比企业科技蓝更细：0.03"）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.81, w: 9.1, h: 0.03,
    fill: { color: theme.border }
  });
  // 左侧草绿强调段（前 0.6"）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.81, w: 0.6, h: 0.03,
    fill: { color: theme.accent }
  });
}
```

### 2. 页码徽章（所有非封面页必用）

```javascript
function addPageBadge(slide, pres, theme, num) {
  // 简约风：方形而非圆形，更克制
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 9.25, y: 5.1, w: 0.4, h: 0.4,
    fill: { color: theme.accent }
  });
  slide.addText(String(num), {
    x: 9.25, y: 5.1, w: 0.4, h: 0.4,
    fontSize: 12, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. 章节分隔页

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 水印数字
  slide.addText(String(num).padStart(2, '0'), {
    x: 0, y: 0.2, w: 6.5, h: 5.2,
    fontSize: 200, fontFace: "Arial Black",
    color: theme.watermark, bold: true, align: "left", margin: 0
  });

  // 草绿竖线装饰（简约风用竖线替代胶囊标签）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 3.5, y: 1.85, w: 0.06, h: 1.2,
    fill: { color: theme.accent }
  });
  // 标题（靠近竖线右侧）
  slide.addText(title, {
    x: 3.72, y: 1.9, w: 5.5, h: 0.6,
    fontSize: 26, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 副标题
  slide.addText(subtitle, {
    x: 3.72, y: 2.6, w: 5.5, h: 0.38,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", margin: 0
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 4. 目录条目（TOC Item）

```javascript
function addTOCItem(slide, pres, theme, x, y, num, title, subtitle, maxW) {
  const numW  = 0.9;
  const numH  = 0.68;
  const divX  = x + numW + 0.05;
  const textX = divX + 0.12;
  const textW = (maxW !== undefined) ? (x + maxW - textX) : (9.55 - textX);

  // 数字：草绿色
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: numW, h: numH,
    fontSize: 36, fontFace: "Arial Black",
    color: theme.accent, bold: true, align: "center", valign: "middle", margin: 0
  });
  // 细竖线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: divX, y: y + 0.1, w: 0.02, h: numH - 0.2,
    fill: { color: theme.border }
  });
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.38,
    fontSize: 15, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "bottom", margin: 0
  });
  slide.addText(subtitle, {
    x: textX, y: y + 0.38, w: textW, h: 0.28,
    fontSize: 11, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", valign: "top", margin: 0
  });
}
```

### 5. 特性条目（Feature Item）

```javascript
function addFeatureItem(slide, pres, theme, x, y, num, title, description, zoneW) {
  const circleSize = 0.38;
  const gap = 0.12;
  const textX = x + circleSize + gap;
  const textW = zoneW - circleSize - gap;

  // 简约风：方形数字块而非圆形
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y + 0.03, w: circleSize, h: circleSize,
    fill: { color: theme.accent }
  });
  slide.addText(String(num), {
    x: x, y: y + 0.03, w: circleSize, h: circleSize,
    fontSize: 13, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.32,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  slide.addText(description, {
    x: textX, y: y + 0.34, w: textW, h: 0.55,
    fontSize: 11, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", valign: "top", margin: 0
  });
}
```

### 6. KPI 指标卡（无边框极简版）

```javascript
function addKPICard(slide, pres, theme, x, y, w, h, value, unit, label, color) {
  // 简约风：无卡片边框，仅用顶部草绿短线区分
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: 0.5, h: 0.04,
    fill: { color: color || theme.accent }
  });
  // 大数字
  slide.addText(value, {
    x: x, y: y + 0.15, w: w, h: 1.0,
    fontSize: 52, fontFace: "Arial Black",
    color: color || theme.accent, bold: true,
    align: "left", valign: "middle", margin: 0
  });
  if (unit) {
    slide.addText(unit, {
      x: x, y: y + 0.8, w: w, h: 0.38,
      fontSize: 15, fontFace: "Microsoft YaHei",
      color: color || theme.accent, bold: true,
      align: "left", margin: 0
    });
  }
  slide.addText(label, {
    x: x, y: y + h - 0.38, w: w - 0.1, h: 0.35,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", margin: 0
  });
}
```

## 5 种页面类型

### Cover（封面）

白色背景，左侧大标题。**不加任何装饰性色块**，仅用一条草绿细线分隔标题和副标题区。

```javascript
slide.background = { color: theme.bg };

// 主标题
slide.addText("报告标题", {
  x: 0.45, y: 1.5, w: 7.0, h: 1.0,
  fontSize: 40, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true, align: "left", margin: 0
});

// 草绿细分隔线
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0.45, y: 2.65, w: 1.2, h: 0.04,
  fill: { color: theme.accent }
});

// 副标题
slide.addText("副标题 / 时间 / 部门", {
  x: 0.45, y: 2.85, w: 6.0, h: 0.45,
  fontSize: 16, fontFace: "Microsoft YaHei",
  color: theme.secondary, align: "left", margin: 0
});
```

### TOC（目录）

左右均分，左侧"目录"大字，右侧 `addTOCItem` 列表。背景 `theme.bg`。

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，背景 `theme.dividerBg`（浅灰，非深色）。

### Content（内容页）

背景统一 `theme.bg`，标题用 `addSlideTitleWithAccent`，页码用 `addPageBadge`。

布局选择：

| 内容关系 | 布局 |
|----------|------|
| 并列要点 3–5 条 | 纯文字 + 每条前方草绿方块小装饰 |
| 对比 / 分析 | 两列，左侧 `theme.light` 浅灰底，右侧白底 |
| KPI 数据 | 横排 2–4 个 `addKPICard`，左对齐 |
| 功能特性 | 左图示 + 右侧 `addFeatureItem` |

### Summary（总结 / 结尾页）

白色背景。中央一行核心结论（大字，草绿色），下方 2–3 行支撑说明（灰色）。保持大量留白，不加装饰。
