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

**内容密度指引（演讲辅助型）：**

> 本风格定位为**产品发布 / 演讲辅助型**，每张幻灯片一个核心观点，信息量适度留白，视觉冲击优先。

- 每张内容页：核心条目 3–5 条，每条一句话（结论导向）
- KPI 页：2–4 个核心数字，大字号显示
- 纯视觉叙事页：允许只有标题 + 1 段短文字 + 大图形元素
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

### TOC（目录）

左半区：大标题"目录"；右半区：用 `addTOCItem` 列条目。背景 `theme.bg`。

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

### Summary（总结 / 结尾页）

背景 `theme.bg`。中央显示核心结论，下方放联系方式或 CTA。可加青绿色大引号作装饰。
