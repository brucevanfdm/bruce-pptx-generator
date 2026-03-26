# Style Preset: Warm Business（暖色商务）

适合场景：培训课程、HR 沟通、团队分享、企业文化、内训材料。让观众感到亲切、易于接受，而非被审阅或考核。

## 氛围

**亲切温暖** — 暖色调、圆角元素、适度色彩、内容结构化但不生硬。传递人情味而非权威感。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深棕蓝 | `2C3E6B` | 标题、主要文字 |
| `secondary` | 暖橙 | `E8834A` | 强调元素、数字、标签、图标色 |
| `accent` | 柔金 | `F5B942` | 标题下方线条、次级高亮、CTA |
| `light` | 米白卡片 | `FFF8F0` | 卡片背景、斑马行 |
| `bg` | 暖白 | `FDFAF7` | 所有内容页背景 |
| `dividerBg` | 浅杏色 | `FFF0E0` | 章节分隔页背景 |
| `bodyText` | 深棕灰 | `3D3D3D` | 正文段落 |
| `mutedText` | 中棕灰 | `7D7060` | 次级文字、说明、描述 |
| `watermark` | 浅暖灰 | `F0E8DC` | 章节分隔页水印数字 |
| `border` | 暖灰线 | `E8DDD0` | 卡片边框、分隔线 |

```javascript
const theme = {
  primary:   "2C3E6B",
  secondary: "E8834A",
  accent:    "F5B942",
  light:     "FFF8F0",
  bg:        "FDFAF7",
  dividerBg: "FFF0E0",
  bodyText:  "3D3D3D",
  mutedText: "7D7060",
  watermark: "F0E8DC",
  border:    "E8DDD0",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 38–44 | Bold | `primary` |
| 封面副标题 | Microsoft YaHei | 17–20 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 26–28 | Bold | `primary` |
| 二级标题 / 卡片标题 | Microsoft YaHei | 15–17 | Bold | `primary` |
| 三级标题 / 特性标题 | Microsoft YaHei | 13–15 | Bold | `secondary` |
| 正文 | Microsoft YaHei | 13–14 | Regular | `bodyText` |
| 说明 / 描述 | Microsoft YaHei | 11–12 | Regular | `mutedText` |
| KPI 大数字 | Arial Black | 44–56 | Bold | `secondary` 或 `accent` |
| TOC 大数字 | Arial Black | 36 | Bold | `secondary` |
| 章节分隔水印数字 | Arial Black | 200 | Bold | `watermark` |
| 标签文字 | Microsoft YaHei | 20–22 | Bold | `FFFFFF` |

## 布局网格系统

幻灯片尺寸 10" × 5.625"，安全边界与企业科技蓝相同。

**暖色风特有规范：**

- 卡片一律使用圆角（`rectRadius: 0.12`），不用直角矩形
- 强调色用暖橙 `secondary`，不用冷蓝
- 间距适度宽松，避免拥挤感

**内容密度指引（培训 / 互动型）：**

> 本风格定位为**培训 / 团队沟通型**，每张幻灯片结构清晰，语气亲切，适合边讲边互动。

- 每张内容页：核心条目 3–5 条，每条 1–2 句，语气主动
- 标题用行动句或疑问句（如"我们为什么这样做？" / "这对你意味着什么"）
- 段落页：每段 2–3 句，语气平实，避免正式书面语
- 允许用 emoji 风格小图标（用文字模拟 ● ▶ ✓ 等）增加亲和感

## 标志性设计元素

### 1. 标题 + 柔金下划线（所有非封面页必用）

圆润感：柔金短线 + 右侧浅暖灰延伸线。

```javascript
function addSlideTitleWithAccent(slide, pres, theme, title) {
  slide.addText(title, {
    x: 0.45, y: 0.22, w: 9.1, h: 0.52,
    fontSize: 26, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 柔金短线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.80, w: 0.5, h: 0.07,
    fill: { color: theme.accent }
  });
  // 右侧浅暖灰延伸线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 1.05, y: 0.83, w: 8.5, h: 0.01,
    fill: { color: theme.border }
  });
}
```

### 2. 页码徽章（所有非封面页必用）

```javascript
function addPageBadge(slide, pres, theme, num) {
  // 暖色风：圆形，暖橙色
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

### 3. 章节分隔页

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 水印大数字
  slide.addText(String(num).padStart(2, '0'), {
    x: 0, y: 0.2, w: 6.5, h: 5.2,
    fontSize: 200, fontFace: "Arial Black",
    color: theme.watermark, bold: true, align: "left", margin: 0
  });

  // 暖橙圆角标签（圆角更大，更圆润）
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fill: { color: theme.secondary },
    rectRadius: 0.34
  });
  slide.addText(title, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fontSize: 22, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });

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
  const numW  = 1.0;
  const numH  = 0.72;
  const divX  = x + numW + 0.05;
  const textX = divX + 0.12;
  const textW = (maxW !== undefined) ? (x + maxW - textX) : (9.55 - textX);

  // 暖橙数字
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: numW, h: numH,
    fontSize: 36, fontFace: "Arial Black",
    color: theme.secondary, bold: true, align: "center", valign: "middle", margin: 0
  });
  // 柔金竖线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: divX, y: y + 0.12, w: 0.04, h: numH - 0.24,
    fill: { color: theme.accent }
  });
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.40,
    fontSize: 16, fontFace: "Microsoft YaHei",
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

  // 暖橙圆形数字
  slide.addShape(pres.shapes.OVAL, {
    x: x, y: y + 0.01, w: circleSize, h: circleSize,
    fill: { color: theme.secondary }
  });
  slide.addText(String(num), {
    x: x, y: y + 0.01, w: circleSize, h: circleSize,
    fontSize: 13, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.32,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  slide.addText(description, {
    x: textX, y: y + 0.34, w: textW, h: 0.72,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", valign: "top", margin: 0
  });
}
```

### 6. KPI 指标卡（圆角暖色版）

```javascript
function addKPICard(slide, pres, theme, x, y, w, h, value, unit, label, color) {
  // 圆角卡片，米白底
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: x, y: y, w: w, h: h,
    fill: { color: theme.light },
    line: { color: theme.border, width: 1 },
    rectRadius: 0.12
  });
  // 顶部暖橙/柔金细条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.07,
    fill: { color: color || theme.secondary }
  });
  // 大数字
  slide.addText(value, {
    x: x, y: y + 0.2, w: w, h: 1.0,
    fontSize: 52, fontFace: "Arial Black",
    color: color || theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  if (unit) {
    slide.addText(unit, {
      x: x, y: y + 0.88, w: w, h: 0.38,
      fontSize: 15, fontFace: "Microsoft YaHei",
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

暖白背景。左侧大标题，底部暖橙色宽色带（装饰性，非全页深色）。

```javascript
slide.background = { color: theme.bg };

// 底部暖橙装饰条
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0, y: 5.0, w: 10, h: 0.625,
  fill: { color: theme.secondary }
});

// 主标题
slide.addText("课程 / 分享标题", {
  x: 0.45, y: 1.3, w: 7.0, h: 1.1,
  fontSize: 40, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true, align: "left", margin: 0
});

// 柔金分隔线
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0.45, y: 2.55, w: 1.5, h: 0.06,
  fill: { color: theme.accent }
});

// 副标题
slide.addText("主讲人  ·  部门  ·  日期", {
  x: 0.45, y: 2.75, w: 6.0, h: 0.45,
  fontSize: 16, fontFace: "Microsoft YaHei",
  color: theme.secondary, align: "left", margin: 0
});
```

### TOC（目录）

左侧"目录"或课程大纲，右侧 `addTOCItem` 列条目。背景 `theme.bg`。

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，背景 `theme.dividerBg`（浅杏色，温暖而非冷灰）。

### Content（内容页）

背景统一 `theme.bg`，标题 `addSlideTitleWithAccent`，页码 `addPageBadge`。

布局选择：

| 内容关系 | 布局 |
|----------|------|
| 并列要点 3–5 条 | 圆角卡片横排，每卡 `theme.light` 底 |
| 步骤 / 流程 | 圆形数字 + 描述，横向或纵向 |
| 对比 / 选择 | 两列圆角卡片，左右各一个场景 |
| 培训要点 | 左侧大问题句，右侧 3 个要点 |
| 数据 / 成效 | `addKPICard` 宫格，数字配暖色强调 |

### Summary（总结 / 结尾页）

暖白背景。中央核心收获（1–2 行大字），下方"感谢参与"或互动引导语。底部可复用封面的暖橙装饰条。
