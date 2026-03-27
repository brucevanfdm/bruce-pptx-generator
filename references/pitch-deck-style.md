# Style Preset: Pitch Deck（路演风）

适合场景：融资路演、产品 Roadmap 向上汇报、Business Case 提案、跨部门拉通。目标是让受众相信你、支持你。

## 氛围

**卖动** — 麦肯锡让人信服于逻辑，Pitch Deck 让人兴奋于可能性。每一页都在回答：为什么要支持这件事？数字要大，主张要清晰，故事弧线要有节奏。

## 色板

| 角色 | 名称 | Hex | 用途 |
|------|------|-----|------|
| `primary` | 深夜蓝 | `0F172A` | 标题、主要文字 |
| `secondary` | 靛蓝 | `6366F1` | 强调色、高亮数字、标签 |
| `accent` | 琥珀橙 | `F59E0B` | CTA、警示、对比强调 |
| `light` | 冷白 | `F1F5F9` | 卡片背景、浅色区块 |
| `bg` | 纯白 | `FFFFFF` | 内容页背景 |
| `dividerBg` | 深夜蓝 | `0F172A` | 暗色章节页背景 |
| `bodyText` | 深板岩 | `1E293B` | 正文段落 |
| `mutedText` | 板岩灰 | `64748B` | 次级文字、说明 |
| `border` | 浅板岩 | `E2E8F0` | 卡片边框、分隔线 |

```javascript
const theme = {
  primary:   "0F172A",
  secondary: "6366F1",
  accent:    "F59E0B",
  light:     "F1F5F9",
  bg:        "FFFFFF",
  dividerBg: "0F172A",
  bodyText:  "1E293B",
  mutedText: "64748B",
  border:    "E2E8F0",
};
```

## 字体规范

| 元素 | 字体 | 大小 (pt) | 粗细 | 颜色 |
|------|------|-----------|------|------|
| 封面主标题 | Microsoft YaHei | 40–50 | Bold | `primary` |
| 封面 Tagline | Microsoft YaHei | 18–22 | Regular | `secondary` |
| 内容页标题 | Microsoft YaHei | 26–32 | Bold | `primary` |
| 章节页标题 | Microsoft YaHei | 36–44 | Bold | `FFFFFF` |
| 二级标题 / 卡片标题 | Microsoft YaHei | 15–18 | Bold | `primary` |
| 正文 | Microsoft YaHei | 12–14 | Regular | `bodyText` |
| 说明 / 注释 | Microsoft YaHei | 10–12 | Regular | `mutedText` |
| 核心数字（Traction） | Arial Black | 52–72 | Bold | `secondary` |
| 次级数字 | Arial Black | 32–44 | Bold | `primary` |
| 标签文字 | Microsoft YaHei | 11–13 | Bold | `FFFFFF`（深色底） |

## 布局网格系统

幻灯片尺寸 10" × 5.625"。

**安全边界：**
- 左/右边距：`0.5"`
- 上边距：`1.1"`（标题区以下）
- 下边距：`0.4"`
- 内容安全区：`x: 0.5–9.5`, `y: 1.1–5.2`

**Pitch Deck 特有结构规范：**
- 前 3 页必须回答：是什么 / 为什么现在 / 你是谁
- 每页有明确的"推进力"——读者看完这页应该更想往下看
- 数字必须是 Traction（真实进展），不是假设预测
- 最后一页必须有 CTA（下一步行动）

**内容密度指引（说服驱动型）：**

> 本风格定位为**说服驱动型**：每张幻灯片一个核心主张，用数字和简洁支撑点证明它。

- 每张内容页：1 个核心主张 + 2–4 个支撑点
- Traction 页：3–5 个大数字，每个配简短标签
- 禁止长段落——超过 2 行的文字必须拆成要点

## 标志性设计元素

### 1. 内容页标题（左侧靛蓝竖条）

Pitch Deck 标志性元素：左侧 4px 靛蓝竖线，强调主张。

```javascript
function addPitchSlideTitle(slide, pres, theme, title) {
  // 左侧靛蓝竖条
  slide.addShape(pres.shapes.RECTANGLE, {
    x: 0.5, y: 0.18, w: 0.07, h: 0.65,
    fill: { color: theme.secondary }
  });
  // 标题
  slide.addText(title, {
    x: 0.68, y: 0.18, w: 8.82, h: 0.65,
    fontSize: 28, fontFace: "Microsoft YaHei",
    color: theme.primary, bold: true,
    align: "left", valign: "middle", margin: 0
  });
}
```

### 2. 页码徽章

```javascript
function addPageBadge(slide, pres, theme, num) {
  // 胶囊形，靛蓝底
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 9.1, y: 5.18, w: 0.55, h: 0.28,
    fill: { color: theme.secondary },
    rectRadius: 0.14
  });
  slide.addText(String(num), {
    x: 9.1, y: 5.18, w: 0.55, h: 0.28,
    fontSize: 11, fontFace: "Arial", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });
}
```

### 3. Traction 数字卡（核心 Metric）

```javascript
function addTractionCard(slide, pres, theme, x, y, w, value, label, growth) {
  // 卡片背景
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 1.7,
    fill: { color: theme.light },
    line: { color: theme.border, width: 0.5 }
  });
  // 顶部靛蓝细线
  slide.addShape(pres.shapes.RECTANGLE, {
    x, y, w, h: 0.06,
    fill: { color: theme.secondary }
  });
  // 核心数字
  slide.addText(value, {
    x: x + 0.1, y: y + 0.15, w: w - 0.2, h: 0.85,
    fontSize: 56, fontFace: "Arial Black",
    color: theme.secondary, bold: true,
    align: "center", valign: "middle", margin: 0
  });
  // 标签
  slide.addText(label, {
    x: x + 0.1, y: y + 1.05, w: w - 0.2, h: 0.3,
    fontSize: 12, fontFace: "Microsoft YaHei",
    color: theme.bodyText, bold: true,
    align: "center", margin: 0
  });
  // 增长标注（可选，琥珀橙）
  if (growth) {
    slide.addText(growth, {
      x: x + 0.1, y: y + 1.38, w: w - 0.2, h: 0.26,
      fontSize: 11, fontFace: "Microsoft YaHei",
      color: theme.accent, bold: true,
      align: "center", margin: 0
    });
  }
}
```

### 4. 章节分隔页（全暗底 + 白色大主张）

```javascript
function createSectionDividerSlide(pres, theme, num, title, subtitle, slideNum) {
  const slide = pres.addSlide();
  slide.background = { color: theme.dividerBg };

  // 靛蓝胶囊标签（章节编号）
  slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
    x: 0.5, y: 1.1, w: 0.95, h: 0.42,
    fill: { color: theme.secondary },
    rectRadius: 0.21
  });
  slide.addText(String(num).padStart(2, '0'), {
    x: 0.5, y: 1.1, w: 0.95, h: 0.42,
    fontSize: 16, fontFace: "Arial Black", color: "FFFFFF",
    bold: true, align: "center", valign: "middle", margin: 0
  });

  // 主标题（白色大字）
  slide.addText(title, {
    x: 0.5, y: 1.7, w: 9.0, h: 1.6,
    fontSize: 40, fontFace: "Microsoft YaHei",
    color: "FFFFFF", bold: true,
    align: "left", valign: "middle", margin: 0
  });

  // 副标题
  if (subtitle) {
    slide.addText(subtitle, {
      x: 0.5, y: 3.5, w: 7.0, h: 0.45,
      fontSize: 16, fontFace: "Microsoft YaHei",
      color: theme.mutedText, align: "left", margin: 0
    });
  }

  addPageBadge(slide, pres, theme, slideNum);
  return slide;
}
```

### 5. 要点列表（带靛蓝方块）

```javascript
function addPitchBullets(slide, pres, theme, x, y, w, items) {
  // items: [{ text, sub }]  sub 是可选的灰色说明
  let curY = y;
  items.forEach(item => {
    // 靛蓝方块
    slide.addShape(pres.shapes.RECTANGLE, {
      x, y: curY + 0.1, w: 0.1, h: 0.1,
      fill: { color: theme.secondary }
    });
    // 主文字
    slide.addText(item.text, {
      x: x + 0.2, y: curY, w: w - 0.2, h: 0.34,
      fontSize: 14, fontFace: "Microsoft YaHei",
      color: theme.bodyText, bold: true,
      align: "left", valign: "middle", margin: 0
    });
    curY += 0.34;
    if (item.sub) {
      slide.addText(item.sub, {
        x: x + 0.2, y: curY, w: w - 0.2, h: 0.26,
        fontSize: 11, fontFace: "Microsoft YaHei",
        color: theme.mutedText,
        align: "left", valign: "top", margin: 0
      });
      curY += 0.3;
    }
    curY += 0.12;
  });
}
```

## 5 种页面类型

### Cover（封面）

白色背景，标题 + Tagline（靛蓝色）。右下角可放公司名或 Logo 占位。

```javascript
slide.background = { color: theme.bg };

slide.addText("项目 / 产品名", {
  x: 0.5, y: 1.2, w: 8.6, h: 1.5,
  fontSize: 48, fontFace: "Microsoft YaHei",
  color: theme.primary, bold: true,
  align: "left", margin: 0
});

slide.addText("一句话说清楚你要做什么", {
  x: 0.5, y: 2.9, w: 7.0, h: 0.6,
  fontSize: 20, fontFace: "Microsoft YaHei",
  color: theme.secondary, align: "left", margin: 0
});

slide.addText("2025  ·  产品部", {
  x: 0.5, y: 5.1, w: 4.0, h: 0.3,
  fontSize: 12, fontFace: "Microsoft YaHei",
  color: theme.mutedText, align: "left", margin: 0
});
```

### TOC（目录）

左侧"议程"深色标题，右侧 3–5 个章节条目（数字 + 标题 + 一行说明）。

### Section Divider（章节分隔）

使用 `createSectionDividerSlide`，全暗底 + 白色主张 + 章节标签。

### Content（内容页）

背景 `theme.bg`，标题用 `addPitchSlideTitle`，页码用 `addPageBadge`。

| 内容关系 | 布局 |
|----------|------|
| 核心 Traction 数据 | 横排 3–4 个 `addTractionCard` |
| 并列要点 / 证据 | `addPitchBullets`，配简短说明 |
| 问题 vs 方案 | 左右两栏，左红/右绿强调 |
| 路线图 / 时间线 | 横向时间轴，靛蓝节点 + 琥珀橙当前位置 |
| 竞争分析 | 象限图或对比表，用靛蓝标出我方优势 |

### Summary（CTA 结尾页）

暗色背景（同分隔页），白色"我们需要什么"大字，下方具体 CTA（金额 / 资源 / 决策），配琥珀橙按钮感文字块。

## Pitch Deck 专项规则

**叙事规则：**
- 故事弧线：痛点 → 机会 → 解决方案 → 证据（Traction）→ 团队 → Ask
- 每页标题是一个有立场的主张，不是中性描述
- Traction 数字必须真实，用 `growth` 字段标明增长方向

**视觉规则：**
- 靛蓝（`secondary`）用于"我们做到了"的正面强调
- 琥珀橙（`accent`）用于"紧迫性"和"行动"，不滥用
- 禁止超过 3 种强调色同时出现在一页
- 章节分隔页必须用暗底（制造节奏感）
