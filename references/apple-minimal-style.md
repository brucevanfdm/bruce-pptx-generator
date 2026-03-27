# Style Preset: Apple 极简（Apple Minimal）

适合场景：产品发布、产品 Demo、Vision 演讲、对外路演、品牌故事。每页一个核心信息，用留白和大字让观众聚焦。

## 氛围

**打动人心** — 极简主义不等于空洞，是把最重要的一件事放到最大、最清晰。每张幻灯片只问一个问题：这页的唯一信息是什么？

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 苹果黑 | `1D1D1F` | 标题、主要文字 |
| `secondary` | 苹果灰 | `6E6E73` | 副标题、说明文字 |
| `accent` | 苹果蓝 | `0071E3` | CTA、强调数字、链接 |
| `light` | 苹果浅灰 | `F5F5F7` | 分隔页背景、卡片底色 |
| `bg` | 纯白 | `FFFFFF` | 所有内容页背景 |
| `dividerBg` | 苹果黑 | `1D1D1F` | 暗色声明页背景 |
| `bodyText` | 深灰 | `3D3D3F` | 正文段落 |
| `mutedText` | 中灰 | `86868B` | 次级说明、注释 |
| `border` | 浅灰线 | `D2D2D7` | 分隔线（极少使用） |

```javascript
const theme = {
  primary:   "1D1D1F",
  secondary: "6E6E73",
  accent:    "0071E3",
  light:     "F5F5F7",
  bg:        "FFFFFF",
  dividerBg: "1D1D1F",
  bodyText:  "3D3D3F",
  mutedText: "86868B",
  border:    "D2D2D7",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 44–56 | Bold | `primary` |
| 封面副标题 | Microsoft YaHei | 18–22 | Regular | `secondary` |
| 声明页大字 | Microsoft YaHei | 40–52 | Bold | `FFFFFF`（暗色背景） |
| 内容页标题 | Microsoft YaHei | 28–34 | Bold | `primary` |
| 单句结论（Hero 页） | Microsoft YaHei | 36–44 | Bold | `primary` |
| 正文 | Microsoft YaHei | 14–16 | Regular | `bodyText` |
| 说明 / 注释 | Microsoft YaHei | 11–13 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 60–80 | Bold | `primary` 或 `accent` |
| 单位 / 标签 | Microsoft YaHei | 16–20 | Regular | `secondary` |

> Apple 风格的核心：**字号要比你以为的更大，内容要比你以为的更少。** 宁可文字只占页面 40%，也不要填满。

## 布局网格系统

幻灯片尺寸 10" × 5.625"。

**安全边界：**
- 左/右边距：`0.6"`（比其他风格更宽，强调留白）
- 上边距：`0.8"`
- 下边距：`0.5"`
- 内容安全区：`x: 0.6–9.4`, `y: 0.8–5.1`

**核心原则：**
- 每页只有一个焦点元素（标题 / 数字 / 图形）
- 其他所有元素都是这个焦点的支撑，不允许喧宾夺主
- 禁止装饰性色块、阴影、渐变——留白本身就是设计
- 文字左对齐或居中二选一，全片统一

**内容密度指引（演讲辅助型）：**

> 本风格定位为**视觉叙事型**：每张幻灯片一句话或一个数字，辅以极少量说明。

- 标题页 / Hero 页：仅标题 + 可选一行副标题
- 数据页：1–3 个 KPI，不要更多
- 要点页：最多 4 条，每条 ≤ 10 字（中文）
- 禁止任何形式的文字墙

## 标志性设计元素

### 1. 内容页标题（极简版，无色块装饰）

```javascript
function addAppleSlideTitle(slide, theme, title) {
  slide.addText(title, {
    x: 0.6, y: 0.25, w: 8.8, h: 0.7,
    fontSize: 30, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });
}
```

### 2. 页码（极简点）

```javascript
function addPageBadge(slide, pres, theme, num) {
  // Apple 风：仅用小灰点 + 数字，无色块
  slide.addText(String(num), {
    x: 9.1, y: 5.2, w: 0.5, h: 0.3,
    fontSize: 11, fontFace: "Arial",
    color: theme.mutedText, align: "center", margin: 0
  });
}
```

### 3. Hero 大字声明（核心页面）

整页只有一句话，居中或左对齐，字号极大。

```javascript
function addHeroStatement(slide, theme, text, color) {
  slide.addText(text, {
    x: 0.6, y: 1.4, w: 8.8, h: 2.8,
    fontSize: 44, fontFace: "Microsoft YaHei",
    color: color || theme.primary, bold: true,
    align: "center", valign: "middle",
    margin: 0, lineSpacingMultiple: 1.2
  });
}
```

### 4. 暗色声明页（Black Statement）

白字深底，用于转场或强调核心主张。

```javascript
function createBlackStatementSlide(pres, theme, text, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  slide.addText(text, {
    x: 0.8, y: 1.3, w: 8.4, h: 2.2,
    fontSize: 42, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "center", valign: "middle", margin: 0, lineSpacingMultiple: 1.2
  });

  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.8, y: 3.7, w: 8.4, h: 0.5,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "center", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 5. KPI 大数字（单指标聚焦）

```javascript
function addAppleKPI(slide, theme, x, y, w, value, unit, label) {
  // 大数字
  slide.addText(value, {
    x, y, w, h: 1.4,
    fontSize: 72, fontFace: "Arial Black",
    color: theme.primary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 单位（紧跟数字右侧，用 offset 实现）
  if (unit) {
    slide.addText(unit, {
      x, y: y + 1.2, w, h: 0.4,
      fontSize: 18, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "center", margin: 0
    });
  }
  // 标签
  slide.addText(label, {
    x, y: y + 1.7, w, h: 0.35,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });
}
```

### 6. 章节分隔页（浅灰底 + 左对齐大标题）

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.light };

  // 蓝色小数字
  slide.addText(String(num).padStart(2, '0'), {
    x: 0.6, y: 1.2, w: 1.5, h: 0.6,
    fontSize: 18, fontFace: "Arial Black",
    color: theme.accent, bold: true, align: "left", margin: 0
  });
  // 大标题
  slide.addText(title, {
    x: 0.6, y: 1.9, w: 8.4, h: 1.4,
    fontSize: 40, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.6, y: 3.45, w: 7.0, h: 0.45,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

## 5 种页面类型

### Cover（封面）

白色背景，主标题占据视觉中心，副标题灰色小字。无任何装饰色块。

```javascript
slide.background = { color: theme.bg };

// 主标题（居中，垂直居中偏上）
slide.addText("产品名称", {
  x: 0.6, y: 1.5, w: 8.8, h: 1.4,
  fontSize: 52, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true,
  align: "center", valign: "middle", margin: 0
});

// 副标题
slide.addText("一句话定位 · 年份", {
  x: 0.6, y: 3.2, w: 8.8, h: 0.5,
  fontSize: 20, fontFace: "Microsoft YaHei",
  color: theme.secondary, align: "center", margin: 0
});
```

### TOC（目录）

极简列表，数字 + 标题，不加任何边框或底色。

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，浅灰背景 + 大标题，或使用 `createBlackStatementSlide` 做暗色强转场。

### Content（内容页）

背景 `theme.bg`，标题用 `addAppleSlideTitle`，内容尽量只用文字，不堆砌色块。

| 内容关系 | 布局 |
|----------|------|
| 单一核心主张 | `addHeroStatement` 居中大字 |
| 1–3 个核心数字 | 横排 `addAppleKPI`，大字居中 |
| 并列要点（≤ 4 条） | 左对齐列表，每条前加 `·` 或蓝色短线 |
| 对比 / Before-After | 左右两栏，极简分隔线 |
| 流程步骤（≤ 4 步） | 横向数字 + 标题 + 一行说明 |

### Summary（结尾页）

暗色背景（`createBlackStatementSlide`），白色大字结论 + 蓝色 CTA 文字。或白色背景 + 超大标题"谢谢"/ 品牌名。

## Apple 风格专项规则

**内容规则：**
- 每张幻灯片只有一个中心信息，读者 3 秒内能理解
- 标题是结论，不是话题（"检测率提升 40%"，不是"检测效果"）
- 禁止在一页内同时出现两个视觉焦点

**视觉规则：**
- 禁止装饰性色块、渐变、阴影
- 禁止文字框描边（除非是数据对比需要区隔）
- 留白面积应占页面 40%–60%
- 所有文字对齐方式全片统一（选左对齐或居中，不混用）
- 色彩克制：一页内最多出现 2 种颜色（不含黑/白/灰）
