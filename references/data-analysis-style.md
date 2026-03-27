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

左侧"本次汇报"标题，右侧条目（章节名 + 核心问题）。

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，深海蓝背景 + 数据蓝竖线装饰。

### Content（内容页）

背景 `theme.bg`，标题用 `addDataSlideTitle`（必须是结论句），页码用 `addPageBadge`。

| 内容关系 | 布局 |
|----------|------|
| 核心 KPI 进展 | 横排 3–5 个 `addKPIChangeCard` |
| 图表 + 分析 | 左 70% 图表占位 + 右 30% `addChartInsight` |
| 对比数据 | 左右两栏，用 `positive`/`accent` 区分好坏 |
| 数据明细 | `addDataTable`，≤ 8 行，超出拆页 |
| 趋势说明 | 横向时间线 + 关键事件标注 |

### Summary（总结页）

白色背景，3–5 条核心发现（用 `addChartInsight` 格式），最后一条是建议行动项（数据蓝加粗）。

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
