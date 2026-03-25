# Style Preset: Corporate Tech Blue（企业科技蓝）

适合场景：AI / 安全 / 产品 / 企业级技术类演示，面向国内政企客户的正式汇报风格。

---

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深海军蓝 | `1A3C6E` | 标题、主要文字、TOC大数字 |
| `secondary` | 亮蓝 | `1E88E5` | 强调元素、数字、胶囊标签、列头 |
| `accent` | 橙色 | `F5782A` | **标题下方橙色短横线（标志性元素）** |
| `light` | 浅蓝 | `E8F4FF` | 卡片背景、浅色填充 |
| `bg` | 白 | `FFFFFF` | 内容页背景 |
| `dividerBg` | 极浅蓝 | `EEF6FF` | 章节分隔页背景 |
| `bodyText` | 深灰 | `333333` | 正文段落 |
| `mutedText` | 中灰 | `666666` | 次级文字、说明、描述 |
| `watermark` | 幽灵蓝 | `C8DEFF` | 章节分隔页超大背景数字 |

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
};
```

---

## 字体

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 40–48 | Bold | `primary` |
| 封面副标题 | Microsoft YaHei | 18–22 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 28–32 | Bold | `primary` |
| TOC 大数字 | Arial Black | 54–64 | Bold | `secondary` |
| 章节分隔水印数字 | Arial Black | 180–220 | Bold | `watermark` |
| 胶囊标签文字 | Microsoft YaHei | 22–26 | Bold | `FFFFFF` |
| 正文 | Microsoft YaHei | 13–15 | Regular | `bodyText` |
| 说明/描述 | Microsoft YaHei | 11–13 | Regular | `mutedText` |
| 总结要点 | Microsoft YaHei | 16–18 | Regular | `bodyText` |

---

## 内容区安全边界

所有内容页的元素必须在此范围内：

```
左边界:   x ≥ 0.45"
右边界:   x + w ≤ 9.55"   （留右侧 0.45" 边距）
上边界:   y ≥ 1.0"         （title + accent bar 底部约 0.9"，留 0.1" 间距）
下边界:   y + h ≤ 5.0"     （页码徽章位于 y:5.1，留 0.1" 间距）
```

常用分区参考（10" 宽）：

| 分区 | x 范围 | 适合内容 |
|------|--------|----------|
| 左半区 | 0.45 – 4.8 | 3D 图标、图表、左侧文字 |
| 右半区 | 5.0 – 9.55 | 特性列表、说明文字 |
| 全宽 | 0.45 – 9.55 | 段落、架构图、宽表格 |
| 左1/3 | 0.45 – 3.5 | 数据大字、图标 |
| 右2/3 | 3.7 – 9.55 | 列表、描述 |

---

## 标志性设计元素

### 1. 标题 + 橙色下划线（所有内容页、案例页必用）

橙色短横条是本风格最核心的标识，每张非封面幻灯片标题下方必须有。

```javascript
function addSlideTitleWithAccent(slide, pres, theme, title) {
  slide.addText(title, {
    x: 0.45, y: 0.22, w: 9.1, h: 0.52,
    fontSize: 30, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", margin: 0
  });
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.82, w: 0.38, h: 0.07,
    fill: { color: theme.accent }
  });
}
```

### 2. 章节分隔页：水印大数字 + 胶囊标签

水印数字从左侧起，胶囊标签居中偏右，描述文字在下方。

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 超大水印数字（从左边界起，装饰性背景层）
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
    fontSize: 24, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });

  // 副标题
  slide.addText(subtitle, {
    x: 3.0, y: 2.78, w: 4.2, h: 0.38,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });

  // 页码徽章
  addPageBadge(slide, pres, theme, slideNum);

  return slide;
}
```

### 3. 目录条目（TOC Item）

大数字 + 竖线分隔 + 标题 + 副标题，右半区排列。

```javascript
function addTOCItem(slide, pres, theme, x, y, num, title, subtitle) {
  // 文字起始 x 和最大宽度（自动适配，不溢出）
  const textX = x + 1.05;
  const textW = 9.55 - textX;

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

// 目录页用法示例（5个条目，x:4.8 开始，间距 0.73"）：
// addTOCItem(slide, pres, theme, 4.8, 0.62, 1, "产品背景", "现状威胁、标准规范");
// addTOCItem(slide, pres, theme, 4.8, 1.35, 2, "产品介绍", "产品概述、4大核心功能");
// addTOCItem(slide, pres, theme, 4.8, 2.08, 3, "部署成效", "产品选型、产品部署、产品成效");
// addTOCItem(slide, pres, theme, 4.8, 2.81, 4, "产品亮点", "核心技术、特色功能");
// addTOCItem(slide, pres, theme, 4.8, 3.54, 5, "案例资质", "实战案例、合作客户");
```

### 4. 蓝色数字特性圆圈 + 特性条目

用于功能特性列表页，右半区排列（左半放 3D 图标）。

```javascript
function addFeatureItem(slide, pres, theme, x, y, num, title, description) {
  // 文字起始 x 和最大宽度（自动适配，不溢出）
  const textX = x + 0.6;
  const textW = 9.55 - textX;

  // 蓝色圆形背景
  slide.addShape(pres.shapes.OVAL, {
    x: x, y: y, w: 0.44, h: 0.44,
    fill: { color: theme.secondary }
  });
  // 圆圈内数字
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: 0.44, h: 0.44,
    fontSize: 13, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // 特性标题（与圆圈垂直居中对齐）
  slide.addText(title, {
    x: textX, y: y, w: textW, h: 0.3,
    fontSize: 16, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 特性描述
  slide.addText(description, {
    x: textX, y: y + 0.32, w: textW, h: 0.6,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", margin: 0
  });
}

// 4个特性，右半区（x:4.5），y 间距 1.1"：
// addFeatureItem(slide, pres, theme, 4.5, 0.95, 1, "多维风险分析", "通过实时风险指标大盘...");
// addFeatureItem(slide, pres, theme, 4.5, 2.05, 2, "事件确认管理", "提供完整的事件处置流程...");
// addFeatureItem(slide, pres, theme, 4.5, 3.15, 3, "调用记录审计", "管理并提供所有调用记录...");
// addFeatureItem(slide, pres, theme, 4.5, 4.25, 4, "操作行为追溯", "完整记录平台管理员操作...");
// 注：第4条 y:4.25 + h:0.32+0.6 = 5.17 → 描述框 h 需缩至 0.45 以留出页码空间
```

### 5. 蓝色列头

用于功能对比页、能力清单列页。

```javascript
function addColumnHeader(slide, pres, theme, x, y, w, text) {
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.42,
    fill: { color: theme.secondary }
  });
  slide.addText(text, {
    x: x, y: y, w: w, h: 0.42,
    fontSize: 15, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 6. 信息卡片（浅蓝背景 + 蓝色条头）

用于案例页各模块（项目背景、核心痛点、应用效果等）。

`bodyLines` 可以是字符串（单段）或 PptxGenJS 富文本数组（多行/混合格式）。
最小高度 `h ≥ 0.7`（条头 0.36 + 内容最小 0.34）。

```javascript
function addInfoCard(slide, pres, theme, x, y, w, h, headerText, bodyLines) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: h,
    fill: { color: theme.light },
    line: { color: "C8DEFF", width: 1 }
  });
  // 蓝色条头
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.36,
    fill: { color: theme.secondary }
  });
  // 条头文字
  slide.addText(headerText, {
    x: x + 0.12, y: y, w: w - 0.14, h: 0.36,
    fontSize: 14, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "left", valign: "middle", margin: 0
  });
  // 卡片内容
  slide.addText(bodyLines, {
    x: x + 0.14, y: y + 0.44, w: w - 0.28, h: h - 0.55,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", margin: 0
  });
}
```

### 7. 页码徽章（辅助函数）

抽出为独立函数，所有非封面页调用。

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

---

## 各页类型布局

### 封面页（Cover）

两种常见变体，选其一保持全场统一。

**变体 A：左文右图（推荐，适合有产品视觉素材时）**

```
| 主标题（大）           |  [深蓝色装饰面板]  |
| 橙色短横线             |  [或3D图标/产品图] |
| 副标题                 |                    |
| 日期 / 场合            |  [公司名/logo]     |
```

```javascript
function createCoverSlide(pres, theme, title, subtitle, dateOrEvent, company) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 右侧深蓝装饰面板
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 6.1, y: 0, w: 3.9, h: 5.625,
    fill: { color: theme.primary }
  });
  // 面板左侧亮蓝竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 6.0, y: 0, w: 0.1, h: 5.625,
    fill: { color: theme.secondary }
  });

  // 主标题
  slide.addText(title, {
    x: 0.45, y: 1.4, w: 5.3, h: 1.6,
    fontSize: 42, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left",
    fit: "shrink", margin: 0
  });
  // 橙色短横线（在副标题上方）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 3.12, w: 0.5, h: 0.07,
    fill: { color: theme.accent }
  });
  // 副标题
  slide.addText(subtitle, {
    x: 0.45, y: 3.25, w: 5.3, h: 0.45,
    fontSize: 18, fontFace: "Microsoft YaHei",
    color: theme.secondary, align: "left", margin: 0
  });
  // 日期/场合
  if (dateOrEvent) {
    slide.addText(dateOrEvent, {
      x: 0.45, y: 3.82, w: 5.3, h: 0.32,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }
  // 右侧面板：公司名
  if (company) {
    slide.addText(company, {
      x: 6.2, y: 4.95, w: 3.5, h: 0.35,
      fontSize: 13, fontFace: "Microsoft YaHei",
      color: "FFFFFF", align: "center", margin: 0
    });
  }

  return slide;
}
```

**变体 B：居中简约（适合演讲开场，无需复杂视觉素材）**

```
|  [顶部深蓝色全宽横幅，含logo区]         |
|                                          |
|         主标题（居中，大）               |
|         橙色短横线（居中）               |
|         副标题（居中）                   |
|                                          |
|  [底部信息栏：日期 / 部门 / 场合]        |
```

```javascript
function createCoverSlideCentered(pres, theme, title, subtitle, dateOrEvent, company) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 顶部深蓝横幅
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 10, h: 1.1,
    fill: { color: theme.primary }
  });
  // 横幅底部亮蓝线条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 1.08, w: 10, h: 0.06,
    fill: { color: theme.secondary }
  });
  // 公司名（横幅内）
  if (company) {
    slide.addText(company, {
      x: 0.5, y: 0, w: 9, h: 1.1,
      fontSize: 18, fontFace: "Microsoft YaHei",
      color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
    });
  }

  // 主标题
  slide.addText(title, {
    x: 0.5, y: 1.6, w: 9, h: 1.4,
    fontSize: 46, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "center",
    fit: "shrink", margin: 0
  });
  // 橙色短横线（居中）
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 4.6, y: 3.12, w: 0.8, h: 0.07,
    fill: { color: theme.accent }
  });
  // 副标题
  slide.addText(subtitle, {
    x: 0.5, y: 3.26, w: 9, h: 0.42,
    fontSize: 20, fontFace: "Microsoft YaHei",
    color: theme.secondary, align: "center", margin: 0
  });

  // 底部信息栏
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 4.95, w: 10, h: 0.675,
    fill: { color: theme.light }
  });
  if (dateOrEvent) {
    slide.addText(dateOrEvent, {
      x: 0.5, y: 4.95, w: 9, h: 0.675,
      fontSize: 14, fontFace: "Microsoft YaHei",
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

- 背景白色 `theme.bg`，右上角可选蓝色斜向波浪装饰（建议 PNG 图片）
- 左侧 3D 图标图片：`x:0.3, y:0.8, w:4.0, h:4.0`
- 顶左："目录" 28pt bold `primary`；下方 "CONTENTS" 22pt `watermark` 色装饰
- 右侧 5 个条目用 `addTOCItem()`，页码徽章用 `addPageBadge()`

### 章节分隔页（Section Divider）

用 `createSectionDividerSlide()` 生成，全部分隔页保持视觉一致。
- 背景 `theme.dividerBg`（`EEF6FF`）
- 底部城市天际线可选（PNG 图片叠加，透明度处理）

### 内容页（Content）

所有内容页共用规则：
- 背景 `theme.bg`（`FFFFFF`），**全部内容页必须使用同一背景值**
- 标题用 `addSlideTitleWithAccent()`
- 内容区从 `y:1.0` 开始，不超过 `y:5.0`
- 页码徽章用 `addPageBadge()`

**子类型选择：**

| 子类型 | 布局 | 适用内容 |
|--------|------|----------|
| 文字分析 | 段落 + 底部双卡片 | 背景/现状分析，带引用截图 |
| 特性列表 | 左侧图标 + 右侧 `addFeatureItem()×4` | 功能详解 |
| 列对比 | `addColumnHeader()` + 列表行 | 能力清单、分类对比 |
| 架构图 | 段落 + 流程图（形状+线条） | 产品架构、系统关系 |
| 数据大字 | 大字号数据 (60–72pt) + 说明文字 | 关键指标、成效数据 |

### 案例页（Case Study）

```
| 标题：应用案例——XX单位AI安全防护        |
| [橙色短横线]                            |
| [项目背景卡片]  |  [核心痛点卡片]       |
|                                         |
| [客户收获：3列图标卡片]                 |
```

- 上半双卡片：`addInfoCard()`，每个卡片 `w:4.5, h:2.2`，左卡 `x:0.45`，右卡 `x:5.1`
- 下方收获区：三列，每列含图标圆圈 + 标题 + 描述
- 页码徽章用 `addPageBadge()`

### 总结/收尾页（Summary / Closing）

三种变体，按场景选择：

**变体 A：核心要点回顾（适合数据/产品汇报）**

```
| 标题：核心亮点   [橙色短横线]           |
|                                         |
|  ① 要点一  ————————————————————————    |
|  ② 要点二  ————————————————————————    |
|  ③ 要点三  ————————————————————————    |
```

```javascript
function createSummarySlide(pres, theme, slideNum, points) {
  // points: [{ num, title, desc }]
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };
  addSlideTitleWithAccent(slide, pres, theme, "核心亮点");

  const startY = 1.1;
  const gap = (4.9 - startY) / points.length;

  points.forEach(({ num, title, desc }, i) => {
    const y = startY + i * gap;
    // 数字圆圈
    slide.addShape(pres.shapes.OVAL, {
      x: 0.45, y: y + 0.05, w: 0.4, h: 0.4,
      fill: { color: theme.secondary }
    });
    slide.addText(String(num).padStart(2, '0'), {
      x: 0.45, y: y + 0.05, w: 0.4, h: 0.4,
      fontSize: 13, fontFace: "Arial", color: "FFFFFF",
      bold: true, align: "center", valign: "middle", margin: 0
    });
    // 分隔线
    slide.addShape(pres.shapes.RECTANGLE, {
      x: 1.0, y: y + 0.24, w: 8.55, h: 0.03,
      fill: { color: theme.light }
    });
    // 标题
    slide.addText(title, {
      x: 1.05, y: y, w: 8.5, h: 0.32,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.primary, bold: true, align: "left", margin: 0
    });
    // 描述
    if (desc) {
      slide.addText(desc, {
        x: 1.05, y: y + 0.33, w: 8.5, h: gap - 0.42,
        fontSize: 13, fontFace: "Microsoft YaHei",
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
|  [步骤1卡片]  [步骤2卡片]  [步骤3卡片] |
|                                         |
|  联系方式：xxx@company.com              |
```

三列卡片：`addInfoCard()`，每个 `w:2.9`，`x` 分别为 `0.45 / 3.55 / 6.65`。
底部联系信息行：`y:4.55, h:0.35, fontSize:14, color: mutedText`。

**变体 C：感谢/Q&A（适合演讲收尾）**

```
|  [左侧深蓝装饰块]  |  感谢聆听          |
|                    |  橙色短横线        |
|                    |  副语（可选）      |
|                    |  联系方式          |
```

```javascript
function createThankYouSlide(pres, theme, slideNum, contactInfo, subtitle) {
  const slide = pres.addSlide();
  slide.background = { color: theme.bg };

  // 左侧深蓝装饰块
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0, y: 0, w: 3.8, h: 5.625,
    fill: { color: theme.primary }
  });
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 3.8, y: 0, w: 0.1, h: 5.625,
    fill: { color: theme.secondary }
  });

  // 右侧：感谢文字
  slide.addText("感谢聆听", {
    x: 4.2, y: 1.4, w: 5.4, h: 1.0,
    fontSize: 48, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", margin: 0
  });
  // 橙色短横线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 4.2, y: 2.55, w: 0.5, h: 0.07,
    fill: { color: theme.accent }
  });
  // 副语
  if (subtitle) {
    slide.addText(subtitle, {
      x: 4.2, y: 2.7, w: 5.4, h: 0.4,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }
  // 联系方式
  if (contactInfo) {
    slide.addText(contactInfo, {
      x: 4.2, y: 3.3, w: 5.4, h: 0.35,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.secondary, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

---

## 注意事项

- **橙色下划线是本风格最重要的标识**，所有非封面幻灯片标题下方不可省略
- **水印数字从 `x:0` 起**，让字符自然填充左侧区域；字体极大时会视觉上超出，这是正常渲染效果
- **分隔页背景统一用 `theme.dividerBg`**，不要在函数内硬编码颜色字符串
- **内容页背景统一用 `theme.bg`**，compile.js 中定义一次，确保所有内容页值相同
- `addTOCItem` 和 `addFeatureItem` 中的文字宽度已自动计算（`9.55 - textX`），无需手动调整
- `addFeatureItem` 第 4 个条目（y:4.25）的描述框高度需缩至 `0.45"` 以避免遮挡页码
- 3D 图标为图片素材，无图时用蓝色圆角矩形叠加形状代替
- 所有中文使用 `Microsoft YaHei`，大数字（TOC、水印）使用 `Arial Black`
- 形状边框：不需要边框时直接省略 `line` 属性；若需明确关闭，使用 `line: { color: theme.bg, width: 0 }`
