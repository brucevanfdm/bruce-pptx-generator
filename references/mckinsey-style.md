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

左侧"目录"深蓝色带 + 右侧议程列表，列表用蓝色数字 + 竖线分隔。

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，深蓝背景，白色标题，左侧亮蓝竖条装饰。

### Content（内容页）

背景 `theme.bg`，全宽深蓝标题栏用 `addMcKinseySlideTitle`（Action Title），页码用 `addPageBadge`。

布局选择：

| 内容关系 | 布局 |
|----------|------|
| 并列要点 3–5 条 | `addBulletSection`，蓝色方块前缀 |
| 对比 / 矩阵分析 | 两列或 2×2 卡片，标题栏蓝色 |
| KPI / 核心指标 | 横排 2–4 个 `addMcKinseyCard` |
| 数据汇总 | `addMcKinseyTable` 斑马行表格 |
| 流程 / 时间线 | 水平箭头流程，蓝色节点 |

### Summary（总结 / 结尾页）

深蓝背景，白色大字结论（居中或左对齐），下方 2–3 条行动建议。保持庄重感，不加多余装饰。

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
- 禁止纯装饰性图形（所有元素必须承载信息）
