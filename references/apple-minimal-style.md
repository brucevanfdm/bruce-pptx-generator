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

**内容密度指引（演讲辅助型 — 精装标准）：**

> 本风格定位为**视觉叙事型**：每张幻灯片一个核心主张，配套数据/洞察和视觉叙事元素。

- 标题页 / Hero 页：仅标题 + 可选一行副标题（可加装饰性几何图形）
- 数据页：1–3 个 KPI，配趋势箭头或变化率标签
- **要点页：3–5 条，每条需有 tagline（10–20 字）+ 底部洞察说明**
- **每张内容页至少包含 1 种非文字视觉**（装饰 SVG / KPI 卡 / 图表 / 图标矩阵）
- 禁止任何形式的文字墙



## 视觉选择决策树

| 内容类型 | 推荐组件（精装优先） |
|---------|---------|
| **核心主张 / 要点页** | **`addAppleRichCard`**（tagline + bullet + 底部洞察） |
| **数据 / KPI 页** | **`addAppleKPI`** + 趋势标签 |
| **对比 / 构成** | `addAppleChart(BAR/PIE)` |
| **流程 / 时间线** | `makeAppleTimeline` (SVG) |
| **层级 / 架构** | `makeAppleHierarchy` (SVG) |
| **并列要点（降级）** | `addAppleBullets` |

**强制规则：**
- **每张 Content 页至少包含 1 种非文字视觉元素**
- 基础 `addHeroStatement` + `addAppleBullets` 视为毛坯房组合，优先用 `addAppleRichCard` 替代

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


### 1.5 精装能力卡片（Rich Card）—— 推荐默认使用

**优先使用此组件替代基础的 `addAppleKPI` + `addAppleBullets` 组合**。精装卡片包含：顶部强调色条、KPI 大数值、单位、tagline、带前缀的 bullet 列表、底部洞察说明区。

```javascript
function addAppleRichCard(slide, pres, theme, x, y, w, h, value, unit, label, tagline, features, detail, highlight) {
  const accentColor = highlight ? theme.accent : theme.secondary;
  const bgColor = theme.light; // Apple 无橙色，高亮通过顶部色条和 accentColor 区分

  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h, fill: { color: bgColor }, line: { color: theme.border, width: 0.5 } });
  // 顶部强调色条
  slide.addShape(pres.shapes.RECTANGLE, { x, y, w, h: 0.07, fill: { color: accentColor } });

  // KPI 大数值
  slide.addText(value, { x: x + 0.1, y: y + 0.18, w: w - 0.2, h: 0.7, fontSize: 38, fontFace: "Arial Black", color: accentColor, bold: true, align: "center", valign: "middle", margin: 0 });
  if (unit) {
    slide.addText(unit, { x: x + w * 0.52, y: y + 0.22, w: w * 0.45, h: 0.26, fontSize: 11, fontFace: "Microsoft YaHei", color: accentColor, bold: true, align: "left", valign: "top", margin: 0 });
  }

  // 标签
  slide.addText(label, { x: x + 0.1, y: y + 0.92, w: w - 0.2, h: 0.3, fontSize: 12, fontFace: "Microsoft YaHei", color: theme.primary, bold: true, align: "center", margin: 0 });

  // Tagline
  slide.addText(tagline, { x: x + 0.1, y: y + 1.24, w: w - 0.2, h: 0.28, fontSize: 9.5, fontFace: "Microsoft YaHei", color: accentColor, align: "center", margin: 0 });

  // 分隔线
  slide.addShape(pres.shapes.LINE, { x: x + 0.1, y: y + 1.58, w: w - 0.2, h: 0, line: { color: theme.border, width: 0.5 } });

  // Bullet 功能列表（带小方块前缀）
  const featStartY = y + 1.66;
  const featH = 0.38;
  features.forEach((f, i) => {
    const fy = featStartY + i * featH;
    slide.addShape(pres.shapes.RECTANGLE, { x: x + 0.12, y: fy + 0.12, w: 0.1, h: 0.1, fill: { color: accentColor } });
    slide.addText(f, { x: x + 0.28, y: fy + 0.05, w: w - 0.42, h: featH - 0.1, fontSize: 9.5, fontFace: "Microsoft YaHei", color: theme.bodyText, align: "left", valign: "middle", margin: 0 });
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

## 2. 页码（极简点）

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

### Cover 精装版（推荐默认使用）

**`createRichCover` — 苹果极简封面精装版。** 遵守"一页只有一个焦点"原则：右侧加单个大数字焦点（或产品核心指标），用细线和留白构成视觉层次，绝不堆砌色块。

```javascript
/**
 * @param {string} title      - 产品/演讲主标题（大字，居中偏左）
 * @param {string} subtitle   - 副标题（一行）
 * @param {string} dateStr    - 日期或演讲者
 * @param {object} spotlight  - 右侧焦点数字，{ value, unit, label }
 *                              例：{ value: "40%", unit: "↑", label: "用户留存提升" }
 *                              如不需要，传 null
 */
function createRichCover(pres, theme, title, subtitle, dateStr, spotlight) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 顶部苹果蓝细线（全宽，极细）
  slide.addShape(pres.shapes.RECTANGLE, { x: 0, y: 0, w: 10, h: 0.04, fill: { color: theme.accent } });

  // 主标题（左对齐，大字）
  slide.addText(title, {
    x: 0.8, y: 1.4, w: spotlight ? 5.4 : 8.4, h: 2.0,
    fontSize: 44, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "top", margin: 0, lineSpaceMult: 1.25
  });

  // 副标题
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.8, y: 3.55, w: 5.4, h: 0.5,
      fontSize: 18, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "left", margin: 0
    });
  }

  // 日期/演讲者
  if (dateStr) {
    slide.addText(dateStr, {
      x: 0.8, y: 5.15, w: 4.0, h: 0.3,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  // 底部全宽细分隔线
  slide.addShape(pres.shapes.RECTANGLE, { x: 0.8, y: 5.08, w: 8.4, h: 0.02, fill: { color: theme.border } });

  // ── 右侧焦点数字（可选）────────────────────────────────────
  if (spotlight) {
    // 垂直分隔线
    slide.addShape(pres.shapes.RECTANGLE, { x: 6.6, y: 1.2, w: 0.02, h: 3.4, fill: { color: theme.border } });

    // 大数字
    slide.addText(spotlight.value, {
      x: 6.85, y: 1.5, w: 2.85, h: 1.8,
      fontSize: 80, fontFace: "Arial Black",
      color: theme.accent, bold: true,
      align: "center", valign: "middle", margin: 0
    });
    // 单位（右上角小字）
    if (spotlight.unit) {
      slide.addText(spotlight.unit, {
        x: 7.5, y: 1.55, w: 1.5, h: 0.4,
        fontSize: 22, fontFace: "Arial Black",
        color: theme.accent, bold: true, align: "left", margin: 0
      });
    }
    // 标签
    slide.addText(spotlight.label, {
      x: 6.85, y: 3.42, w: 2.85, h: 0.42,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "center", margin: 0
    });
  }

  return slide;
}
```

**调用示例：**
```javascript
// 有焦点数字版
createRichCover(pres, theme,
  "重新定义\n医疗随访体验",
  "AI 智能随访平台 · 产品发布",
  "2025年 04月",
  { value: "95%", unit: "+", label: "随访完成率" }
);

// 纯极简版（无焦点数字）
createRichCover(pres, theme, "人人都能用的 AI", "产品路线图 2025", "April 2025", null);
```

### TOC（目录）

极简列表，数字 + 标题，不加任何边框或底色。

```javascript
function createAppleTOCSlide(pres, theme, items, slideNum) {
  // items: [{ num, title, subtitle? }]，最多 6 条
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 页面标题
  slide.addText("目录", {
    x: 0.6, y: 0.3, w: 8.8, h: 0.55,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.muted, align: "left", valign: "middle", margin: 0
  });
  // 细分隔线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.6, y: 0.9, w: 8.8, h: 0.01,
    fill: { color: theme.border }
  });

  const n = Math.min(items.length, 6);
  const rowH = (5.0 - 1.05) / n;  // 均分内容区

  items.slice(0, n).forEach((item, i) => {
    const ry = 1.05 + i * rowH;
    const isLast = i === n - 1;

    // 序号（蓝色，Arial Black）
    slide.addText(String(item.num).padStart(2, "0"), {
      x: 0.6, y: ry, w: 0.9, h: rowH,
      fontSize: 22, fontFace: "Arial Black",
      color: theme.secondary, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    // 标题
    slide.addText(item.title, {
      x: 1.6, y: ry, w: 7.8, h: item.subtitle ? rowH * 0.55 : rowH,
      fontSize: 15, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true,
      align: "left", valign: item.subtitle ? "bottom" : "middle", margin: 0
    });
    // 副标题（可选）
    if (item.subtitle) {
      slide.addText(item.subtitle, {
        x: 1.6, y: ry + rowH * 0.55, w: 7.8, h: rowH * 0.38,
        fontSize: 11, fontFace: "Microsoft YaHei",
        color: theme.muted, align: "left", valign: "top", margin: 0
      });
    }
    // 条目底部分隔线（最后一条不加）
    if (!isLast) {
      slide.addShape(pres.shapes.RECTANGLE, {
        x: 1.6, y: ry + rowH - 0.01, w: 7.8, h: 0.01,
        fill: { color: theme.border }
      });
    }
  });

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}

// 用法（5 章节）：
// createAppleTOCSlide(pres, theme, [
//   { num: 1, title: "背景与挑战",   subtitle: "市场变化与核心痛点" },
//   { num: 2, title: "解决方案",     subtitle: "产品核心能力全景" },
//   { num: 3, title: "实施路径",     subtitle: "三阶段落地方案" },
//   { num: 4, title: "成效与案例",   subtitle: "客户验证数据" },
//   { num: 5, title: "下一步",       subtitle: "行动建议与资源投入" },
// ], 2);
```

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
