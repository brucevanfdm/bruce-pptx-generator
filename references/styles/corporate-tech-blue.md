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
| `bg` | 白 | `FFFFFF` | 幻灯片背景 |
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
  bodyText:  "333333",
  mutedText: "666666",
  watermark: "C8DEFF",
};
```

---

## 字体

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 幻灯片标题 | Microsoft YaHei | 28–32 | Bold | `primary` |
| TOC 大数字 | Arial Black | 56–64 | Bold | `secondary` |
| 章节分隔水印数字 | Arial Black | 180–220 | Bold | `watermark` |
| 胶囊标签文字 | Microsoft YaHei | 22–26 | Bold | `FFFFFF` |
| 正文 | Microsoft YaHei | 13–15 | Regular | `bodyText` |
| 说明/描述 | Microsoft YaHei | 11–13 | Regular | `mutedText` |

---

## 标志性设计元素

### 1. 标题 + 橙色下划线（所有内容页必用）

橙色短横条是本风格最核心的标识，每张内容页标题下方必须有。

```javascript
function addSlideTitleWithAccent(slide, pres, theme, title) {
  // 标题文字
  slide.addText(title, {
    x: 0.45, y: 0.22, w: 9, h: 0.52,
    fontSize: 30, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", margin: 0
  });
  // 橙色下划线短横条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.45, y: 0.82, w: 0.38, h: 0.07,
    fill: { color: theme.accent }, line: { color: theme.accent, width: 0 }
  });
}
```

### 2. 章节分隔页：水印大数字 + 胶囊标签

水印数字占满左侧背景，胶囊标签居中偏右，描述文字在下方。

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle) {
  const slide = pres.addSlide();
  slide.background = { color: "EEF6FF" }; // 极浅蓝背景

  // 超大水印数字（背景层）
  slide.addText(String(num).padStart(2, '0'), {
    x: -0.5, y: 0.3, w: 7, h: 5,
    fontSize: 200, fontFace: "Arial Black",
    color: theme.watermark, bold: true, align: "left", margin: 0
  });

  // 胶囊标签背景
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fill: { color: theme.secondary },
    rectRadius: 0.34,  // 完整胶囊
    line: { color: theme.secondary, width: 0 }
  });
  // 胶囊标签文字
  slide.addText(title, {
    x: 3.6, y: 1.9, w: 3.0, h: 0.68,
    fontSize: 24, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true, align: "center", valign: "middle", margin: 0
  });

  // 副标题
  slide.addText(subtitle, {
    x: 3.0, y: 2.78, w: 4.0, h: 0.38,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "center", margin: 0
  });

  return slide;
}
```

### 3. 目录条目（TOC Item）

大数字 + 竖线分隔 + 标题 + 副标题，是本风格目录页的核心结构。

```javascript
function addTOCItem(slide, pres, theme, x, y, num, title, subtitle) {
  // 大数字
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: 0.85, h: 0.65,
    fontSize: 54, fontFace: "Arial Black",
    color: theme.secondary, bold: true, align: "right", valign: "middle", margin: 0
  });
  // 竖分隔线
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x + 0.9, y: y + 0.09, w: 0.04, h: 0.5,
    fill: { color: theme.secondary }, line: { color: theme.secondary, width: 0 }
  });
  // 标题
  slide.addText(title, {
    x: x + 1.05, y: y, w: 4.5, h: 0.36,
    fontSize: 17, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "bottom", margin: 0
  });
  // 副标题
  slide.addText(subtitle, {
    x: x + 1.05, y: y + 0.35, w: 4.5, h: 0.28,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.mutedText, align: "left", valign: "top", margin: 0
  });
}

// 目录页用法示例（5个条目，右半区域，x从4.8开始）：
// addTOCItem(slide, pres, theme, 4.8, 0.62, 1, "产品背景", "现状威胁、标准规范");
// addTOCItem(slide, pres, theme, 4.8, 1.35, 2, "产品介绍", "产品概述、4大核心功能");
// addTOCItem(slide, pres, theme, 4.8, 2.08, 3, "部署成效", "产品选型、产品部署、产品成效");
// addTOCItem(slide, pres, theme, 4.8, 2.81, 4, "产品亮点", "核心技术、特色功能");
// addTOCItem(slide, pres, theme, 4.8, 3.54, 5, "案例资质", "实战案例、合作客户");
```

### 4. 蓝色数字特性圆圈 + 特性条目

用于功能特性列表页，左侧蓝色圆圈数字，右侧标题+描述。

```javascript
function addFeatureItem(slide, pres, theme, x, y, num, title, description) {
  // 蓝色圆形背景
  slide.addShape(pres.shapes.OVAL, {
    x: x, y: y, w: 0.44, h: 0.44,
    fill: { color: theme.secondary }, line: { color: theme.secondary, width: 0 }
  });
  // 圆圈内数字
  slide.addText(String(num).padStart(2, '0'), {
    x: x, y: y, w: 0.44, h: 0.44,
    fontSize: 13, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
  // 特性标题
  slide.addText(title, {
    x: x + 0.6, y: y - 0.02, w: 6.5, h: 0.3,
    fontSize: 16, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true, align: "left", valign: "middle", margin: 0
  });
  // 特性描述
  slide.addText(description, {
    x: x + 0.6, y: y + 0.3, w: 6.5, h: 0.5,
    fontSize: 13, fontFace: "Microsoft YaHei",
    color: theme.bodyText, align: "left", margin: 0
  });
}

// 4个特性的标准间距（y依次 +1.1）：
// addFeatureItem(slide, pres, theme, 4.2, 0.9, 1, "多维风险分析：精准洞察与识别潜在威胁", "...");
// addFeatureItem(slide, pres, theme, 4.2, 2.0, 2, "事件确认管理：全流程闭环处置与追踪", "...");
// addFeatureItem(slide, pres, theme, 4.2, 3.1, 3, "调用记录审计：全面记录与审查对话内容", "...");
// addFeatureItem(slide, pres, theme, 4.2, 4.2, 4, "操作行为追溯：保障系统安全与合规", "...");
```

### 5. 蓝色列头

用于功能对比页、能力清单列页。

```javascript
function addColumnHeader(slide, pres, theme, x, y, w, text) {
  slide.addShape(pres.shapes.RECTANGLE, {
    x: x, y: y, w: w, h: 0.42,
    fill: { color: theme.secondary }, line: { color: theme.secondary, width: 0 }
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
    fill: { color: theme.secondary }, line: { color: theme.secondary, width: 0 }
  });
  // 条头文字
  slide.addText(headerText, {
    x: x + 0.12, y: y, w: w - 0.12, h: 0.36,
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

---

## 各页类型布局

### 目录页（TOC）

```
| [3D图标/左半区] | 目录 (bold, primary)          |
|                | CONTENTS (light watermark)     |
|                | 01 | 产品背景   现状威胁…        |
|                | 02 | 产品介绍   产品概述…        |
|                | 03 | 部署成效   产品选型…        |
|                | 04 | 产品亮点   核心技术…        |
|                | 05 | 案例资质   实战案例…        |
```

- 背景白色，右上角可选蓝色斜向波浪条（建议用图片素材）
- 左侧放3D等距图标图片（x:0.3, y:0.8, w:4, h:4）
- 顶部左侧："目录" 28pt bold primary，下方 "CONTENTS" 22pt watermark色作装饰
- 右侧5个TOC条目用 `addTOCItem()`

### 章节分隔页（Section Divider）

```
| [超大水印数字，左侧背景]                |
|              [ 胶囊标签：章节标题 ]    |
|              描述副标题文字            |
| [淡色城市天际线，底部，可选]           |
```

- 背景极浅蓝 `EEF6FF`
- 用 `createSectionDividerSlide()` 生成
- 底部城市图可选（作为PNG图片加入）

### 内容页（Content）

```
| 标题文字                              |
| [橙色短横线]                          |
|                                       |
| [内容区，根据子类型选择布局]          |
|                                       |
| [底部极浅蓝渐变条，可选]              |
```

- 每页用 `addSlideTitleWithAccent()` 添加标题
- 内容区子类型：
  - **文字+图表**：左侧图表，右侧结论列表
  - **特性列表**：左侧3D图标 + 右侧 `addFeatureItem()` × 4
  - **列对比**：`addColumnHeader()` + 行列表
  - **架构图**：文字段落 + 流程图（用形状和线条构建）

### 案例页（Case Study）

```
| 标题：应用案例——某某单位AI安全防护    |
| [橙色短横线]                          |
| [项目背景卡片] | [核心痛点卡片]        |
|                                       |
| [应用效果，3列图标卡片]               |
| [客户收获，2-3列]                     |
```

- 使用 `addInfoCard()` 构建各模块卡片
- 效果图标卡片：蓝色圆圈图标 + 白色描述

---

## 注意事项

- **橙色下划线是本风格最重要的标识**，内容页标题下方不可省略
- 水印数字只用 `watermark` 色（浅蓝），不要用透明度来降低对比——PptxGenJS文字无直接透明度属性
- 3D图标为图片素材，无图时用蓝色圆角矩形叠加形状代替
- 右上角蓝色斜向波浪条（目录页装饰）建议用 PNG 图片引入，纯形状难以精确还原曲线
- 所有中文一律使用 `Microsoft YaHei`，英文数字可混用 `Arial Black`（大数字）
