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
| TOC 大数字 | Arial Black | 42 | Bold | `secondary` |
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

**内容密度指引（客户汇报型，看完即懂）：**

> 本风格定位为**客户汇报型 PPT**，目标是让客户看完幻灯片就能理解内容，而非辅助演讲者讲话。优先信息传达密度，**不适用精简演讲风**。

- 每张内容页：正文条目 4–7 条，每条描述 2–3 行（完整语义句，非关键词堆砌）
- 每张对比页：列数 ≤ 4，行数 ≤ 8；单元格内容可写 1–2 句完整说明
- 每张 KPI 页：指标数 ≤ 4（2×2 或 4×1），每卡片必须包含单位 + 标签 + 1 行说明
- 纯文字段落页：字数 150–220 字，段落 3–4 段，每段 2–4 句完整表述
- 特性/功能描述：标题 + 2–3 行说明（阐明原理或效果，避免只写功能名称）
- 不允许在同一区域同时出现 4 种以上颜色
- 避免内容过少：每张幻灯片信息量应足够客户无需听讲解也能自行阅读理解

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
  // maxW: 条目总宽度（右边界 = x + maxW）
  // 数字区宽度固定 1.1"，文字区从 x+1.22 开始
  const numW  = 1.1;
  const numH  = 0.72;
  const divX  = x + numW + 0.05;          // 竖线紧贴数字区右侧
  const textX = divX + 0.12;              // 文字区起点（竖线右侧留 0.12" 间距）
  const textW = (maxW !== undefined) ? (x + maxW - textX) : (9.55 - textX);

  // 大数字（字号缩小至 42，确保在高度 0.72" 内完整显示，居中对齐防止截断）
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: numW, h: numH,
    fontSize: 42, fontFace: "Arial Black",
    color: theme.secondary, bold: true, align: "center", valign: "middle", margin: 0
  });
  // 竖分隔线（与数字区垂直居中对齐）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: divX, y: y + 0.11, w: 0.04, h: numH - 0.22,
    fill: { color: theme.secondary }
  });
  // 标题
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.40,
    fontSize: 17, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "bottom", margin: 0
  });
  // 副标题
  slide.addText(subtitle, {
    x: textX, y: y + 0.40, w: textW, h: 0.30,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", valign: "top", margin: 0
  });
}

// 目录页用法示例（5个条目，x:4.6 开始，条目总宽 4.95"，行距 0.85"）：
// 每行高度 = 0.72"，行距 0.85"，5 条总高 = 4*0.85+0.72 = 4.12"，起始 y:0.55，底部 4.67" ≤ 5.0" ✓
// addTOCItem(slide, pres, theme, 4.6, 0.55, 1, "产品背景", "现状威胁、标准规范与行业挑战", 4.95);
// addTOCItem(slide, pres, theme, 4.6, 1.40, 2, "产品介绍", "产品概述、4大核心功能模块", 4.95);
// addTOCItem(slide, pres, theme, 4.6, 2.25, 3, "部署成效", "产品选型、部署方案与实测成效", 4.95);
// addTOCItem(slide, pres, theme, 4.6, 3.10, 4, "产品亮点", "核心技术创新与特色功能详解", 4.95);
// addTOCItem(slide, pres, theme, 4.6, 3.95, 5, "案例资质", "实战案例、合作客户与行业认证", 4.95);
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
  // 特性描述（支持 2–3 行完整说明，阐明原理或实际效果）
  slide.addText(description, {
    x: textX, y: y + 0.34, w: textW, h: 0.72,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", valign: "top", margin: 0
  });
}

// 每条特性高度 = 标题 0.34 + 描述 0.72 = 1.06"；description 写 2–3 句完整说明
//
// ── 4条特性（行距 0.96"，紧凑但不溢出）──────────────────────────────────
// 验算：y4=3.93, bottom=3.93+1.06=4.99 ≤ 5.0 ✓
// addFeatureItem(slide, pres, theme, 5.1, 1.05, 1, "多维风险分析", "聚合多源数据计算综合风险评分，安全团队可直观掌握全局威胁态势，快速定位高危资产与薄弱环节。", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 2.01, 2, "事件确认管理", "提供告警分级、责任人指派与处置记录全流程，确保每条告警有据可查，平均响应时间缩短 60%。", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 2.97, 3, "调用记录审计", "全量采集所有 API 调用日志，支持多维度回溯审计，满足等保 2.0 审计要求，留存期可配置。", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 3.93, 4, "操作行为追溯", "完整记录管理员操作轨迹，结合异常行为检测模型，自动识别越权操作与内部风险行为。", 4.45);
//
// ── 3条特性（行距 1.25"，描述可更丰富）──────────────────────────────────
// 验算：y3=3.55, bottom=3.55+1.06=4.61 ≤ 5.0 ✓
// addFeatureItem(slide, pres, theme, 5.1, 1.05, 1, "智能威胁感知", "...", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 2.30, 2, "自动化响应", "...", 4.45);
// addFeatureItem(slide, pres, theme, 5.1, 3.55, 3, "合规审计报告", "...", 4.45);
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
- 右侧 5 个条目用 `addTOCItem()`，`x:4.6, maxW:4.95`，起始 `y:0.55`，行距 `0.85"`
- **注意**：数字字号 42pt，条目行高 0.72"，行间距 0.85"；右边界 x+maxW = 9.55"，严格不超出
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

| 子类型 | 函数/组件 | 典型用途 | 关系类型 |
|--------|-----------|----------|----------|
| 并列卡片 | `addParallelCards()` | 功能对比、特点列举、场景分类 | 并列（对等、无先后） |
| 总分布局 | `addHierarchicalLayout()` | 总体概述+子项展开、一对多 | 总分（整体含子项） |
| 带箭头流程 | `addFlowProcess()` | 实施步骤、操作流程 | 顺序（有先后依赖） |
| 循环布局 | `addCycleLayout()` | PDCA、迭代周期、相互依存 | 循环（首尾相连） |
| 金字塔布局 | `addPyramid()` | 层级结构、战略到执行 | 层级/优先级 |
| 特性列表 | `addFeatureItem()×3-4` | 功能模块详解 | 并列 |
| KPI 指标 | `addKPICard()` | 成效数据、关键指标 | 并列 |
| 痛点分析 | `addInfoCard()×3` | 客户痛点、挑战场景 | 并列 |
| 对比矩阵 | `addColumnHeader()` + 行列数据 | 能力对比、方案选型 | 对比 |
| 数据大字 | 大字号数据 (56–72pt) + 说明 | 单指标突出展示 | — |

**内容布局识别原则（根据内容关系自动选型）：**

> 读完内容后先判断条目之间的关系，再选布局函数。禁止选"看起来好看"的布局而忽视内容逻辑。

| 如果内容是… | 选哪种布局 |
|-------------|------------|
| 几个对等的功能/特点/场景，无先后顺序 | G1 并列卡片 |
| 一个主概念下分 2-4 个子项 | G2 总分布局 |
| 有明确先后顺序的步骤 | G3 带箭头流程 |
| 相互促进/依赖、首尾相连 | G4 循环布局 |
| 有高低层级、从战略到执行 | G5 金字塔布局 |

**禁止留白过多**：所有图形布局必须填满内容区 `y:1.05–5.0`。每个方框内文字：标题 14–16pt bold + 正文 12–13pt，正文写 2–3 行完整语义句，不写单词/关键词。

**痛点分析页（3列卡片）布局示例：**

```javascript
// 3 列均等卡片（w:2.87，间距 0.2"），高度 h:2.8
// addInfoCard(slide, pres, theme, 0.45, 1.15, 2.87, 2.8, "痛点一：数据孤岛", "各系统数据分散...");
// addInfoCard(slide, pres, theme, 3.52, 1.15, 2.87, 2.8, "痛点二：响应滞后", "告警处理依赖人工...");
// addInfoCard(slide, pres, theme, 6.59, 1.15, 2.96, 2.8, "痛点三：合规压力", "等保 2.0 要求...");
```

### 图形布局组件

> **通用规则**：所有函数中 `startY` 默认 `1.05`，`endY` 默认 `5.0`。函数内部自动计算列宽、行高，填满内容区，无需手动调整坐标。

#### G1. 并列卡片 addParallelCards

**适用**：并列关系（对等的功能/特点/场景/优势），2–4 列。

卡片结构：蓝色条头（标题）+ 浅蓝背景（正文），正文深色文字，确保可读性。

```javascript
/**
 * @param {Array} items - [{ title, body }] 2-4条，body 写 2-3 行完整语义句
 * @param {number} startY - 内容区起始 y，默认 1.05
 */
function addParallelCards(slide, pres, theme, items, startY) {
  startY = startY || 1.05;
  const n = items.length;
  const totalW = 9.1;
  const gap = 0.2;
  const cardW = (totalW - gap * (n - 1)) / n;
  const cardH = 5.0 - startY;

  items.forEach((item, i) => {
    const x = 0.45 + i * (cardW + gap);
    // 卡片背景
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: startY, w: cardW, h: cardH,
      fill: { color: theme.light },
      line: { color: theme.border, width: 1 }
    });
    // 蓝色条头
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: startY, w: cardW, h: 0.46,
      fill: { color: theme.secondary }
    });
    // 序号圆点（左侧）
    slide.addShape(pres.shapes.OVAL, {
      x: x + 0.12, y: startY + 0.08, w: 0.3, h: 0.3,
      fill: { color: "FFFFFF", transparency: 30 }
    });
    slide.addText(String(i + 1), {
      x: x + 0.12, y: startY + 0.08, w: 0.3, h: 0.3,
      fontSize: 12, fontFace: "Arial Black",
      color: theme.secondary, bold: true, align: "center", valign: "middle", margin: 0
    });
    // 条头标题（序号右侧）
    slide.addText(item.title, {
      x: x + 0.5, y: startY, w: cardW - 0.6, h: 0.46,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: "FFFFFF", bold: true, align: "left", valign: "middle", margin: 0
    });
    // 正文（条头下方，深色文字保证可读性）
    slide.addText(item.body, {
      x: x + 0.16, y: startY + 0.56, w: cardW - 0.32, h: cardH - 0.66,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.bodyText, align: "left", valign: "top",
      lineSpacingMultiple: 1.3, margin: 0
    });
  });
}

// 3列用法（startY 默认 1.05，卡片高 3.95"）：
// addParallelCards(slide, pres, theme, [
//   { title: "威胁感知", body: "实时采集终端、网络、云环境的安全事件，通过机器学习模型识别隐藏威胁，覆盖率达 98%。支持自定义规则库，适配各类业务场景。" },
//   { title: "智能响应", body: "基于剧本化自动化处置引擎，在威胁确认后 30 秒内完成隔离、阻断等响应动作，显著缩短 MTTR。" },
//   { title: "合规审计", body: "全量记录安全事件处置过程，自动生成等保 2.0、行业监管所需的审计报告，减少人工整理工作量 80%。" },
// ]);
```

**坐标验算（3列，startY=1.05）**：
- cardW = (9.1-0.4)/3 = 2.9，cardH = 3.95
- col0 right = 0.45+2.9 = 3.35 | col1 right = 3.55+2.9 = 6.45 | col2 right = 6.65+2.9 = 9.55 ✓
- 卡片底 = 1.05+3.95 = 5.0 ✓

#### G2. 总分布局 addHierarchicalLayout

**适用**：一个主概念+2–4 个子项展开，强调从整体到局部。

结构：顶部全宽深蓝主框（总）→ 连接器 → 底部等宽子卡片（分）。

```javascript
/**
 * @param {string} mainTitle - 顶部主框左侧标题（精简，12字以内）
 * @param {string} mainBody  - 顶部主框右侧说明文字（1-2 句完整表述）
 * @param {Array}  subs      - [{ title, body }] 2-4条子项
 */
function addHierarchicalLayout(slide, pres, theme, mainTitle, mainBody, subs) {
  const n = subs.length;
  const mainH = 1.1;
  const connectorY = 1.05 + mainH;          // 2.15
  const connH = 0.5;
  const subY = connectorY + connH;           // 2.65
  const subH = 5.0 - subY;                  // 2.35
  const subW = (9.1 - 0.2 * (n - 1)) / n;
  const centerX = 5.0;

  // ── 主框（全宽，深蓝背景）────────────────────────────
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 1.05, w: 9.1, h: mainH,
    fill: { color: theme.primary }
  });
  // 左侧橙色竖条（标志性元素）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 1.05, w: 0.08, h: mainH,
    fill: { color: theme.accent }
  });
  // 主标题
  slide.addText(mainTitle, {
    x: 0.65, y: 1.05, w: 2.8, h: mainH,
    fontSize: 18, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "left", valign: "middle", margin: 0
  });
  // 主说明文字
  slide.addText(mainBody, {
    x: 3.55, y: 1.05, w: 5.9, h: mainH,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: "E8F4FF", align: "left", valign: "middle",
    lineSpacingMultiple: 1.3, margin: 0
  });

  // ── 连接器（主框 → 子框）───────────────────────────
  // 主垂线（从主框底边中心向下）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: centerX - 0.02, y: connectorY, w: 0.04, h: connH * 0.45,
    fill: { color: theme.border }
  });
  // 水平线（连接各子框顶部中心）
  const firstCx = 0.45 + subW / 2;
  const lastCx  = 0.45 + (n - 1) * (subW + 0.2) + subW / 2;
  slide.addShape(pres.shapes.RECTANGLE, {
    x: firstCx, y: connectorY + connH * 0.45, w: lastCx - firstCx, h: 0.03,
    fill: { color: theme.border }
  });
  // 各子框顶部垂线
  subs.forEach((_, i) => {
    const cx = 0.45 + i * (subW + 0.2) + subW / 2;
    slide.addShape(pres.shapes.RECTANGLE, {
      x: cx - 0.02, y: connectorY + connH * 0.45, w: 0.04, h: connH * 0.55,
      fill: { color: theme.border }
    });
  });

  // ── 子卡片（浅蓝背景，深色文字）───────────────────
  subs.forEach((sub, i) => {
    const x = 0.45 + i * (subW + 0.2);
    // 卡片背景
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: subY, w: subW, h: subH,
      fill: { color: theme.light },
      line: { color: theme.border, width: 1 }
    });
    // 蓝色条头
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: subY, w: subW, h: 0.4,
      fill: { color: theme.secondary }
    });
    slide.addText(sub.title, {
      x: x + 0.1, y: subY, w: subW - 0.2, h: 0.4,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
    });
    // 子卡正文
    slide.addText(sub.body, {
      x: x + 0.14, y: subY + 0.50, w: subW - 0.28, h: subH - 0.60,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: theme.bodyText, align: "left", valign: "top",
      lineSpacingMultiple: 1.3, margin: 0
    });
  });
}

// 3子项用法：
// addHierarchicalLayout(slide, pres, theme,
//   "AI 安全防护平台",
//   "以人工智能为核心引擎，构建覆盖感知、研判、响应全链路的自动化安全防护体系，面向政企客户提供开箱即用的安全能力。",
//   [
//     { title: "威胁感知层", body: "通过多源日志融合与行为基线学习，实时识别异常流量和用户行为。内置 200+ 攻击指纹，0day 检出率提升 40%。" },
//     { title: "智能研判层", body: "利用图神经网络关联事件上下文，将误报率降低至 5% 以内，每日自动处置告警 5000+，节省分析师 80% 精力。" },
//     { title: "自动响应层", body: "剧本化编排 30 余种响应动作，支持与主流安全设备联动，平均响应时间由 4 小时压缩至 2 分钟。" },
//   ]
// );
```

**坐标验算（3子项）**：
- mainBox: y=1.05, bottom=2.15 | subY=2.65, subH=2.35, bottom=5.0 ✓
- subW = (9.1-0.4)/3 = 2.9；col2 right = 6.65+2.9 = 9.55 ✓

#### G3. 带箭头流程 addFlowProcess

**适用**：有先后顺序的步骤（实施路径、操作流程），3–4 步。

全高方框（填满内容区），步骤间用橙色箭头衔接，正文描述详细操作内容。

```javascript
/**
 * @param {Array} items - [{ title, body }] 3-4步，body 写具体操作内容/产出物
 */
function addFlowProcess(slide, pres, theme, items) {
  const n = items.length;
  const arrowSp = 0.2;                           // 箭头占 0.2" 间距
  const stepW = (9.1 - arrowSp * (n - 1)) / n;  // 动态计算步骤宽度
  const stepY = 1.1;
  const stepH = 3.9;                             // 填满 y:1.1–5.0
  const colors = [theme.primary, theme.secondary, theme.primary, theme.secondary];

  items.forEach((item, i) => {
    const x = 0.45 + i * (stepW + arrowSp);
    const bg = colors[i % colors.length];

    // 步骤方框（交替深蓝/亮蓝）
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: stepY, w: stepW, h: stepH,
      fill: { color: bg }
    });

    // 顶部步骤编号圆圈
    const circleSize = 0.52;
    const cx = x + stepW / 2 - circleSize / 2;
    slide.addShape(pres.shapes.OVAL, {
      x: cx, y: stepY + 0.22, w: circleSize, h: circleSize,
      fill: { color: "FFFFFF", transparency: 20 }
    });
    slide.addText(String(i + 1), {
      x: cx, y: stepY + 0.22, w: circleSize, h: circleSize,
      fontSize: 18, fontFace: "Arial Black",
      color: bg, bold: true, align: "center", valign: "middle", margin: 0
    });

    // 步骤标题
    slide.addText(item.title, {
      x: x + 0.1, y: stepY + 0.86, w: stepW - 0.2, h: 0.52,
      fontSize: 15, fontFace: "Microsoft YaHei",
      color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
    });

    // 分隔线
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + 0.22, y: stepY + 1.44, w: stepW - 0.44, h: 0.02,
      fill: { color: "FFFFFF", transparency: 55 }
    });

    // 步骤正文（填充剩余高度）
    slide.addText(item.body, {
      x: x + 0.16, y: stepY + 1.54, w: stepW - 0.32, h: stepH - 1.64,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: "E8F4FF", align: "left", valign: "top",
      lineSpacingMultiple: 1.4, margin: 0
    });

    // 橙色箭头（连接到下一步，文字字符居中于间隔区）
    if (i < n - 1) {
      slide.addText("▶", {
        x: x + stepW - 0.02, y: stepY + stepH / 2 - 0.2, w: arrowSp + 0.04, h: 0.4,
        fontSize: 16, fontFace: "Arial",
        color: theme.accent, bold: true, align: "center", valign: "middle", margin: 0
      });
    }
  });
}

// 4步用法（stepW ≈ 2.11"，stepH=3.9"）：
// addFlowProcess(slide, pres, theme, [
//   { title: "需求调研", body: "与业务部门深度访谈，梳理现有安全架构痛点、合规差距与核心诉求。产出：需求确认书、差距分析报告。" },
//   { title: "方案设计", body: "依据调研结论制定分层安全防护架构，规划感知、研判、响应三层模块边界与接口规范。产出：架构方案书。" },
//   { title: "部署实施", body: "分阶段完成环境准备、系统安装、数据源接入与联调测试，全程提供专属实施顾问支持。产出：上线验收报告。" },
//   { title: "运营交付", body: "提供 3 个月常驻运营支持，建立安全运营规程，完成核心人员培训，确保客户团队独立运营能力。" },
// ]);
//
// 3步用法（stepW ≈ 2.9"，更宽，可写更多正文）：
// addFlowProcess(slide, pres, theme, [
//   { title: "现状评估", body: "..." },
//   { title: "能力建设", body: "..." },
//   { title: "持续优化", body: "..." },
// ]);
```

**坐标验算（4步）**：stepW=(9.1-0.6)/4=2.125；last x=0.45+3*2.325=7.425，right=9.55 ✓；bottom=1.1+3.9=5.0 ✓

#### G4. 循环布局 addCycleLayout

**适用**：4 个环节首尾相连、相互依存（PDCA、监控→告警→响应→复盘 等循环模式）。

2×2 方格，橙色方向箭头标示循环方向，中心椭圆放循环标签。

```javascript
/**
 * @param {string} centerLabel - 中心标签文字（2-4字，如"持续循环"）
 * @param {Array}  items       - [{ title, body }] 固定4条，顺时针：左上→右上→右下→左下
 */
function addCycleLayout(slide, pres, theme, centerLabel, items) {
  const cardW = 4.0, cardH = 1.6;
  const gapX = 1.1, gapY = 0.75;
  const leftX = 0.45, rightX = leftX + cardW + gapX;  // 5.55
  const topY  = 1.05, botY  = topY  + cardH + gapY;   // 3.40

  // [右边界 9.55 ✓ 底边 5.0 ✓]
  const positions = [
    { x: leftX,  y: topY, color: theme.primary },    // 0: 左上
    { x: rightX, y: topY, color: theme.secondary },  // 1: 右上
    { x: rightX, y: botY, color: theme.primary },    // 2: 右下
    { x: leftX,  y: botY, color: theme.secondary },  // 3: 左下
  ];

  // 中心椭圆标签
  const elW = 0.9, elH = 0.65;
  const elX = leftX + cardW + gapX / 2 - elW / 2;   // 4.6
  const elY = topY  + cardH + gapY / 2 - elH / 2;   // 2.725
  slide.addShape(pres.shapes.OVAL, {
    x: elX, y: elY, w: elW, h: elH,
    fill: { color: theme.accent }
  });
  slide.addText(centerLabel || "循环", {
    x: elX, y: elY, w: elW, h: elH,
    fontSize: 11, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });

  // 4条方向箭头（顺时针）
  const midTopY   = topY + cardH / 2;
  const midBotY   = botY + cardH / 2;
  const midLeftX  = leftX  + cardW / 2;
  const midRightX = rightX + cardW / 2;

  // → 左上到右上（水平顶部）
  slide.addText("▶", {
    x: leftX + cardW, y: midTopY - 0.18, w: gapX, h: 0.36,
    fontSize: 18, fontFace: "Arial", color: theme.accent,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // ↓ 右上到右下（垂直右侧）
  slide.addText("▼", {
    x: midRightX - 0.18, y: topY + cardH, w: 0.36, h: gapY,
    fontSize: 18, fontFace: "Arial", color: theme.accent,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // ← 右下到左下（水平底部）
  slide.addText("◀", {
    x: leftX + cardW, y: midBotY - 0.18, w: gapX, h: 0.36,
    fontSize: 18, fontFace: "Arial", color: theme.accent,
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // ↑ 左下到左上（垂直左侧）
  slide.addText("▲", {
    x: midLeftX - 0.18, y: topY + cardH, w: 0.36, h: gapY,
    fontSize: 18, fontFace: "Arial", color: theme.accent,
    bold: true, align: "center", valign: "middle", margin: 0
  });

  // 4张卡片
  items.forEach((item, i) => {
    const { x, y, color } = positions[i];

    // 卡片背景
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y, w: cardW, h: cardH,
      fill: { color }
    });
    // 顶部装饰细条（橙色，增强辨识度）
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y, w: cardW, h: 0.05,
      fill: { color: theme.accent }
    });

    // 序号
    slide.addText(String(i + 1).padStart(2, '0'), {
      x: x + 0.14, y: y + 0.1, w: 0.55, h: 0.42,
      fontSize: 22, fontFace: "Arial Black",
      color: "FFFFFF", bold: true,
      align: "left", valign: "top", margin: 0
    });
    // 标题（序号右侧，右对齐）
    slide.addText(item.title, {
      x: x + 0.14, y: y + 0.1, w: cardW - 0.28, h: 0.42,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: "FFFFFF", bold: true, align: "right", valign: "top", margin: 0
    });
    // 正文
    slide.addText(item.body, {
      x: x + 0.18, y: y + 0.60, w: cardW - 0.36, h: cardH - 0.70,
      fontSize: 12, fontFace: "Microsoft YaHei",
      color: "E8F4FF", align: "left", valign: "top",
      lineSpacingMultiple: 1.3, margin: 0
    });
  });
}

// 用法示例（PDCA 循环）：
// addCycleLayout(slide, pres, theme, "持续改进", [
//   { title: "Plan 规划", body: "识别安全风险，制定季度防护目标与资源计划，分解至各专项团队。" },
//   { title: "Do 执行", body: "按计划开展渗透测试、配置加固、员工培训等安全建设工作，记录执行日志。" },
//   { title: "Check 检查", body: "通过红蓝对抗与合规扫描验证防护效果，输出指标达成情况分析报告。" },
//   { title: "Act 改进", body: "根据检查结论修订策略、补充规则库，将成功实践固化为标准操作流程。" },
// ]);
```

**坐标验算**：rightX+cardW=9.55 ✓ | botY+cardH=5.0 ✓ | 箭头在 gapX/gapY 区域内，不与卡片重叠 ✓

#### G5. 金字塔布局 addPyramid

**适用**：层级结构、优先级高低、从战略（顶层窄）到基础（底层宽）。

3–5 层矩形，宽度从上到下递增，居中对齐。每层左侧写标题、右侧写说明。

```javascript
/**
 * @param {Array} items - [{ title, desc }]，index 0 = 顶层（最窄/最重要），最后一条 = 底层（最宽/基础）
 *                        建议 3–5 条；顶层用 accent 色，往下渐变为 primary / secondary
 */
function addPyramid(slide, pres, theme, items) {
  const n = items.length;
  const minW = 2.2;                          // 顶层宽度
  const maxW = 9.1;                          // 底层宽度（填满内容区）
  const startY = 1.05, endY = 5.0;
  const totalH = endY - startY;             // 3.95"
  const rowH = totalH / n;                  // 每行占用高度（含间距）
  const layerH = rowH - 0.04;              // 实际矩形高度（留 0.04" 间隙）

  // 颜色：顶层 accent（橙，最显眼），往下变为深蓝/亮蓝
  const layerColors = [
    theme.accent,     // 顶层
    theme.primary,
    theme.secondary,
    "#3D8FD8",
    "#6AAEE6",
  ];
  const textColors  = ["FFFFFF", "FFFFFF", "FFFFFF", "FFFFFF", "FFFFFF"];

  items.forEach((item, i) => {
    // 宽度从顶到底线性增大
    const fraction = n === 1 ? 1 : i / (n - 1);
    const w = minW + (maxW - minW) * fraction;
    const x = 0.45 + (maxW - w) / 2;        // 水平居中
    const y = startY + i * rowH;
    const color = layerColors[i % layerColors.length];
    const textColor = textColors[i % textColors.length];

    // 层背景
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y, w, h: layerH,
      fill: { color }
    });
    // 左侧白色竖细条（增强分层感）
    slide.addShape(pres.shapes.RECTANGLE, {
      x: x + 0.14, y: y + 0.1, w: 0.04, h: layerH - 0.2,
      fill: { color: "FFFFFF", transparency: 50 }
    });

    // 层标题（左区域）
    const titleW = Math.min(w * 0.38, 3.2);
    slide.addText(item.title, {
      x: x + 0.26, y, w: titleW, h: layerH,
      fontSize: 15, fontFace: "Microsoft YaHei",
      color: textColor, bold: true, align: "left", valign: "middle", margin: 0
    });

    // 层描述（右区域，仅当层宽足够时显示）
    if (item.desc && w > 3.5) {
      slide.addText(item.desc, {
        x: x + titleW + 0.36, y, w: w - titleW - 0.5, h: layerH,
        fontSize: 12, fontFace: "Microsoft YaHei",
        color: textColor, align: "left", valign: "middle",
        lineSpacingMultiple: 1.3, margin: 0
      });
    }
  });
}

// 4层用法（顶层=战略，底层=基础设施）：
// addPyramid(slide, pres, theme, [
//   { title: "战略目标",  desc: "构建行业领先的 AI 驱动安全运营体系，实现安全与业务深度融合。" },
//   { title: "安全能力",  desc: "威胁感知、智能研判、自动响应、合规审计四大核心能力全面覆盖。" },
//   { title: "平台支撑",  desc: "统一数据底座 + 开放 API 生态，无缝对接主流安全设备与 SIEM 平台。" },
//   { title: "基础设施",  desc: "高可用集群部署，支持私有云、混合云、信创环境，99.95% SLA 保障。" },
// ]);
//
// 3层用法（层更高，每层可写更多描述）：
// addPyramid(slide, pres, theme, [
//   { title: "决策层",   desc: "..." },
//   { title: "管理层",   desc: "..." },
//   { title: "执行层",   desc: "..." },
// ]);
```

**坐标验算（4层，rowH=0.9875，layerH=0.9575）**：
- layer0(顶): w=2.2, x=3.9, y=1.05, bottom=2.01 ✓
- layer3(底): w=9.1, x=0.45, y=4.02, bottom=4.98 ✓，右边 9.55 ✓

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
