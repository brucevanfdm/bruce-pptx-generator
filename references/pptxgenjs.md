# PptxGenJS 教程

## 安装与基本结构

```javascript
const pptxgen = require("pptxgenjs");

let pres = new pptxgen();
pres.layout = 'LAYOUT_16x9';  // 或 'LAYOUT_16x10', 'LAYOUT_4x3', 'LAYOUT_WIDE'
pres.author = 'Your Name';
pres.title = 'Presentation Title';

let slide = pres.addSlide();
slide.addText("Hello World!", { x: 0.5, y: 0.5, fontSize: 36, color: "363636" });

pres.writeFile({ fileName: "Presentation.pptx" });
```

## 版面尺寸

幻灯片尺寸（坐标单位为英寸）：
- `LAYOUT_16x9`：10" x 5.625"（默认）
- `LAYOUT_16x10`：10" x 6.25"
- `LAYOUT_4x3`：10" x 7.5"
- `LAYOUT_WIDE`：13.3" x 7.5"

## Slide Master 与 Placeholder

当 deck 有统一品牌元素、固定标题区、页脚、页码轨道、图表区或表格区时，优先使用 Slide Master，而不是在每张幻灯片中重复绘制。

### 定义 Master

```javascript
const pptxgen = require("pptxgenjs");
const pres = new pptxgen();

pres.defineSlideMaster({
  title: "CONTENT_MASTER",
  background: { color: "FFFFFF" },
  objects: [
    { rect: { x: 0, y: 0, w: "100%", h: 0.7, fill: { color: "F8FAFC" } } },
    { line: { x: 0.6, y: 0.9, w: 8.8, h: 0, line: { color: "1E88E5", width: 1.5 } } },
    {
      placeholder: {
        options: { name: "title", type: "title", x: 0.6, y: 0.22, w: 7.8, h: 0.36 },
        text: "(title placeholder)",
      },
    },
    {
      placeholder: {
        options: { name: "body", type: "body", x: 0.6, y: 1.15, w: 4.0, h: 3.4 },
        text: "(body placeholder)",
      },
    },
    {
      placeholder: {
        options: { name: "chart", type: "chart", x: 4.9, y: 1.15, w: 4.4, h: 3.4 },
      },
    },
  ],
  slideNumber: { x: 9.2, y: 5.1, color: "64748B", fontFace: "Arial", fontSize: 10 },
});
```

使用时，把 master 名称传给 `addSlide()`：

```javascript
const slide = pres.addSlide({ masterName: "CONTENT_MASTER" });
```

### 使用 Placeholder

在 master 中先声明 placeholder，再通过 `placeholder` 名称填充内容：

```javascript
const slide = pres.addSlide({ masterName: "CONTENT_MASTER" });

slide.addText("AI triage cut follow-up delays by 37%", {
  placeholder: "title",
});

slide.addText([
  { text: "3 pilot hospitals online", options: { bullet: true, breakLine: true } },
  { text: "Median wait time down from 54m to 34m", options: { bullet: true } },
], {
  placeholder: "body",
});

slide.addChart(pres.charts.BAR, [{
  name: "Wait Time",
  labels: ["Before", "After"],
  values: [54, 34],
}], {
  placeholder: "chart",
});
```

### Placeholder 类型

PptxGenJS 官方支持以下 placeholder type：

| type | 用途 |
|------|------|
| `title` | 标题 |
| `body` | 正文区 |
| `image` | 图片 |
| `chart` | 图表 |
| `table` | 表格 |
| `media` | 音视频 |

**建议**：在 skill 中稳定使用 `title`、`subtitle`、`body`、`chart`、`table`、`insight`、`media` 这些命名。视觉风格可以变化，但槽位语义不要漂移。

## Sections（章节）

当 deck 有目录、章节分隔页和附录时，优先把结构同步到 PowerPoint section，而不是只做视觉上的“章节页”。

```javascript
const pptxgen = require("pptxgenjs");
const pres = new pptxgen();

pres.addSection({ title: "Market Opportunity" });
pres.addSection({ title: "Solution" });
pres.addSection({ title: "Appendix" });

const slide = pres.addSlide({
  masterName: "CONTENT_MASTER",
  sectionTitle: "Solution",
});

slide.addText("This slide belongs to the Solution section.", {
  x: 1,
  y: 1,
  w: 6,
  h: 0.4,
  fontSize: 20,
  color: "1F2937",
});
```

**建议：**

- 封面、目录页可不归属 section
- 章节分隔页、内容页、总结页、附录页应显式指定 `sectionTitle`
- TOC 文案、Section Divider 标题、`addSection({ title })` 的标题保持一致

## 文字与格式

```javascript
// 基本文字
slide.addText("Simple Text", {
  x: 1, y: 1, w: 8, h: 2, fontSize: 24, fontFace: "Arial",
  color: "363636", bold: true, align: "center", valign: "middle"
});

// 字符间距（使用 charSpacing，letterSpacing 会被静默忽略）
slide.addText("SPACED TEXT", { x: 1, y: 1, w: 8, h: 1, charSpacing: 6 });

// 富文字数组
slide.addText([
  { text: "Bold ", options: { bold: true } },
  { text: "Italic ", options: { italic: true } }
], { x: 1, y: 3, w: 8, h: 1 });

// 多行文字（需要 breakLine: true）
slide.addText([
  { text: "Line 1", options: { breakLine: true } },
  { text: "Line 2", options: { breakLine: true } },
  { text: "Line 3" }  // 最后一项不需要 breakLine
], { x: 0.5, y: 0.5, w: 8, h: 2 });

// 文字框内边距
slide.addText("Title", {
  x: 0.5, y: 0.3, w: 9, h: 0.6,
  margin: 0  // 需要文字与形状或图标精确对齐时设为 0
});
```

**提示：** 文字框默认有内边距。当需要文字与同一 x 位置的形状、线条或图标精确对齐时，请设置 `margin: 0`。

## 列表与项目符号

```javascript
// 正确：多个项目符号
slide.addText([
  { text: "First item", options: { bullet: true, breakLine: true } },
  { text: "Second item", options: { bullet: true, breakLine: true } },
  { text: "Third item", options: { bullet: true } }
], { x: 0.5, y: 0.5, w: 8, h: 3 });

// 错误：不要使用 Unicode 项目符号
slide.addText("* First item", { ... });  // 会产生双重项目符号

// 子项目与编号列表
{ text: "Sub-item", options: { bullet: true, indentLevel: 1 } }
{ text: "First", options: { bullet: { type: "number" }, breakLine: true } }
```

## 形状

```javascript
slide.addShape(pres.shapes.RECTANGLE, {
  x: 0.5, y: 0.8, w: 1.5, h: 3.0,
  fill: { color: "FF0000" }, line: { color: "000000", width: 2 }
});

slide.addShape(pres.shapes.OVAL, { x: 4, y: 1, w: 2, h: 2, fill: { color: "0000FF" } });

slide.addShape(pres.shapes.LINE, {
  x: 1, y: 3, w: 5, h: 0, line: { color: "FF0000", width: 3, dashType: "dash" }
});

// 带透明度
slide.addShape(pres.shapes.RECTANGLE, {
  x: 1, y: 1, w: 3, h: 2,
  fill: { color: "0088CC", transparency: 50 }
});

// 圆角矩形（rectRadius 只对 ROUNDED_RECTANGLE 有效，不适用于 RECTANGLE）
// 不要搭配矩形强调色覆盖层——矩形覆盖层无法遮住圆角。请改用 RECTANGLE。
slide.addShape(pres.shapes.ROUNDED_RECTANGLE, {
  x: 1, y: 1, w: 3, h: 2,
  fill: { color: "FFFFFF" }, rectRadius: 0.1
});

// 带阴影
slide.addShape(pres.shapes.RECTANGLE, {
  x: 1, y: 1, w: 3, h: 2,
  fill: { color: "FFFFFF" },
  shadow: { type: "outer", color: "000000", blur: 6, offset: 2, angle: 135, opacity: 0.15 }
});
```

阴影选项：

| 属性 | 类型 | 范围 | 说明 |
|----------|------|-------|-------|
| `type` | string | `"outer"`, `"inner"` | |
| `color` | string | 6 位十六进制（如 `"000000"`） | 不加 `#` 前缀，不使用 8 位十六进制——参见常见陷阱 |
| `blur` | number | 0-100 pt | |
| `offset` | number | 0-200 pt | **必须为非负值**——负值会损坏文件 |
| `angle` | number | 0-359 度 | 阴影投射方向（135 = 右下，270 = 向上） |
| `opacity` | number | 0.0-1.0 | 用于控制透明度，不要将透明度编码进颜色字符串 |

若要向上投射阴影（例如底部栏），请使用 `angle: 270` 搭配正数 offset——**不要**使用负数 offset。

**注意**：不原生支持渐变填充。请改用渐变图片作为背景。

## 图片

### 图片来源

```javascript
// 从文件路径
slide.addImage({ path: "images/chart.png", x: 1, y: 1, w: 5, h: 3 });

// 从 URL
slide.addImage({ path: "https://example.com/image.jpg", x: 1, y: 1, w: 5, h: 3 });

// 从 base64（更快，无文件 I/O）
slide.addImage({ data: "image/png;base64,iVBORw0KGgo...", x: 1, y: 1, w: 5, h: 3 });
```

### 图片选项

```javascript
slide.addImage({
  path: "image.png",
  x: 1, y: 1, w: 5, h: 3,
  rotate: 45,              // 0-359 度
  rounding: true,          // 圆形裁切
  transparency: 50,        // 0-100
  flipH: true,             // 水平翻转
  flipV: false,            // 垂直翻转
  altText: "Description",  // 无障碍描述
  hyperlink: { url: "https://example.com" }
});
```

### 图片尺寸模式

`sizing.type` 支持 `'contain'`（保持比例适应容器）、`'cover'`（填满裁切）、`'crop'`（指定裁切区域）。

### 计算尺寸（保持宽高比）

```javascript
const origWidth = 1978, origHeight = 923, maxHeight = 3.0;
const calcWidth = maxHeight * (origWidth / origHeight);
const centerX = (10 - calcWidth) / 2;

slide.addImage({ path: "image.png", x: centerX, y: 1.2, w: calcWidth, h: maxHeight });
```

### 支持的格式

- **标准格式**：PNG、JPG、GIF（动态 GIF 在 Microsoft 365 中可用）
- **SVG**：在现代 PowerPoint / Microsoft 365 中可用

## 图标

使用 react-icons 生成 SVG 图标，再转为 PNG 以获得最佳兼容性。

**重要**：图标生成是异步的，但 `createSlide()` 必须是同步的。请在调用 `createSlide()` 之前预先生成所有图标数据，再作为参数传入或存入外部作用域的变量中。

### 模式：在 compile.js 中预生成图标并传入 createSlide

```javascript
// 在 compile.js 中（此处允许使用异步上下文）
const { iconToBase64Png } = require("./icon-utils");
const { FaCheckCircle } = require("react-icons/fa");

// 在创建幻灯片之前预先生成
const checkIcon = await iconToBase64Png(FaCheckCircle, "#4472C4", 256); // react-icons 接受 CSS 颜色格式（含 #），这是唯一允许使用 # 前缀的地方；addShape/addText 颜色仍禁止 #

// 作为额外参数传入
const slideModule = require("./slide-03.js");
slideModule.createSlide(pres, theme, { checkIcon });
```

```javascript
// 在 slide-03.js 中
function createSlide(pres, theme, icons = {}) {
  const slide = pres.addSlide();
  if (icons.checkIcon) {
    slide.addImage({ data: icons.checkIcon, x: 1, y: 1, w: 0.5, h: 0.5 });
  }
  return slide;
}
```

### 图标库

安装：`npm install -g react-icons react react-dom sharp`

react-icons 中常用的图标集：
- `react-icons/fa` — Font Awesome
- `react-icons/md` — Material Design
- `react-icons/hi` — Heroicons
- `react-icons/bi` — Bootstrap Icons

## 幻灯片背景

```javascript
// 纯色
slide.background = { color: "F1F1F1" };

// 带透明度的颜色
slide.background = { color: "FF3399", transparency: 50 };

// 来自 URL 的图片
slide.background = { path: "https://example.com/bg.jpg" };

// 来自 base64 的图片
slide.background = { data: "image/png;base64,iVBORw0KGgo..." };
```

## 表格

```javascript
slide.addTable([
  ["Header 1", "Header 2"],
  ["Cell 1", "Cell 2"]
], {
  x: 1, y: 1, w: 8, h: 2,
  border: { pt: 1, color: "999999" }, fill: { color: "F1F1F1" }
});

// 进阶用法：合并单元格
let tableData = [
  [{ text: "Header", options: { fill: { color: "6699CC" }, color: "FFFFFF", bold: true } }, "Cell"],
  [{ text: "Merged", options: { colspan: 2 } }]
];
slide.addTable(tableData, { x: 1, y: 3.5, w: 8, colW: [4, 4] });
```

### 表格自动分页（Appendix 推荐）

长表格不要硬塞在内容页里。PptxGenJS 原生支持 `autoPage`，适合附录明细表：

```javascript
slide.addTable(tableRows, {
  placeholder: "table",
  autoPage: true,
  autoPageRepeatHeader: true,
  autoPageHeaderRows: 1,
  newSlideStartY: 1.15,
  border: { pt: 1, color: "CBD5E1" },
  fill: { color: "FFFFFF" },
  fontFace: "Microsoft YaHei",
  fontSize: 10,
});
```

关键选项：

- `autoPage: true`：表格溢出时自动创建后续幻灯片
- `autoPageRepeatHeader: true`：每页重复表头
- `autoPageHeaderRows: 1`：多行表头时，指定重复几行
- `newSlideStartY`：续页表格从新的 y 位置开始，避免浪费空间

**使用建议：**

- 内容页保留结论摘要和小表；长明细表直接移入 appendix
- Appendix 页优先使用专门的 `APPENDIX_MASTER`
- 表格一旦需要缩到 10pt 以下才能塞进内容页，就已经应该拆到 appendix

### HTML 表格导出（备选）

如果明细表天然存在于网页 DOM 中，也可以使用 `tableToSlides()` 直接生成 1–N 页 PPT 表格：

```javascript
pptx.tableToSlides("myHtmlTableID", {
  master: "APPENDIX_MASTER",
});
```

这条路径更适合“已有 HTML 表格”的场景；当前 skill 的代码生成路径仍优先使用 `addTable(..., { autoPage: true })`。

## 图表

```javascript
// 条形图
slide.addChart(pres.charts.BAR, [{
  name: "Sales", labels: ["Q1", "Q2", "Q3", "Q4"], values: [4500, 5500, 6200, 7100]
}], {
  x: 0.5, y: 0.6, w: 6, h: 3, barDir: 'col',
  showTitle: true, title: 'Quarterly Sales'
});

// 折线图
slide.addChart(pres.charts.LINE, [{
  name: "Temp", labels: ["Jan", "Feb", "Mar"], values: [32, 35, 42]
}], { x: 0.5, y: 4, w: 6, h: 3, lineSize: 3, lineSmooth: true });

// 饼图
slide.addChart(pres.charts.PIE, [{
  name: "Share", labels: ["A", "B", "Other"], values: [35, 45, 20]
}], { x: 7, y: 1, w: 5, h: 4, showPercent: true });
```

### 更美观的图表

默认图表样式较为过时。应用以下选项可获得现代简洁的外观：

```javascript
slide.addChart(pres.charts.BAR, chartData, {
  x: 0.5, y: 1, w: 9, h: 4, barDir: "col",

  // 自定义颜色（与演示文稿调色板保持一致）
  chartColors: ["0D9488", "14B8A6", "5EEAD4"],

  // 干净的背景
  chartArea: { fill: { color: "FFFFFF" }, roundedCorners: true },

  // 柔和的坐标轴标签
  catAxisLabelColor: "64748B",
  valAxisLabelColor: "64748B",

  // 细腻的网格线（仅数值轴）
  valGridLine: { color: "E2E8F0", size: 0.5 },
  catGridLine: { style: "none" },

  // 在柱体上显示数据标签
  showValue: true,
  dataLabelPosition: "outEnd",
  dataLabelColor: "1E293B",

  // 单数据系列时隐藏图例
  showLegend: false,
});
```

**关键样式选项：**
- `chartColors: [...]` — 系列/分段的十六进制颜色
- `chartArea: { fill, border, roundedCorners }` — 图表背景
- `catGridLine/valGridLine: { color, style, size }` — 网格线（`style: "none"` 可隐藏）
- `lineSmooth: true` — 曲线（折线图）
- `legendPos: "r"` — 图例位置："b"、"t"、"l"、"r"、"tr"

## 常见陷阱

以下问题会导致文件损坏、视觉错误或输出异常。版面与内容方面的错误请参见 [qa.md](qa.md)。

1. **绝对不要在十六进制颜色中使用 "#"** — 会导致文件损坏
   ```javascript
   color: "FF0000"      // 正确
   color: "#FF0000"     // 错误——会损坏文件
   ```

2. **绝对不要将不透明度编码进十六进制颜色字符串** — 8 位十六进制（如 `"00000020"`）会损坏文件；请改用 `opacity` 属性
   ```javascript
   shadow: { color: "00000020" }                          // 损坏文件
   shadow: { color: "000000", opacity: 0.12 }             // 正确
   ```

3. **使用 `bullet: true`** — 不要使用 Unicode 项目符号如 `"•"`（会产生双重项目符号）

4. **在数组项目或文字段之间使用 `breakLine: true`** 以实现换行

5. **避免在项目符号中使用 `lineSpacing`** — 会造成过大间距；请改用 `paraSpaceAfter`

6. **每个演示文稿需要新的实例** — 不要跨调用复用 `pptxgen()` 对象

7. **绝对不要跨调用复用选项对象** — PptxGenJS 会就地修改对象（将阴影值转换为 EMU）。在多个 `addShape` 调用中共享同一对象会损坏第二个形状。
   ```javascript
   // 错误——第二次调用时获取到已被修改的值
   const shadow = { type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 };
   slide.addShape(pres.shapes.RECTANGLE, { shadow });
   slide.addShape(pres.shapes.RECTANGLE, { shadow });

   // 正确——工厂函数每次返回新对象
   const makeShadow = () => ({ type: "outer", blur: 6, offset: 2, color: "000000", opacity: 0.15 });
   slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow() });
   slide.addShape(pres.shapes.RECTANGLE, { shadow: makeShadow() });
   ```

8. **不要将 `ROUNDED_RECTANGLE` 与强调色边框覆盖层搭配使用** — 矩形条无法干净地覆盖圆角；请改用 `RECTANGLE`
   ```javascript
   // 错误
   slide.addShape(pres.shapes.ROUNDED_RECTANGLE, { x:1, y:1, w:3, h:1.5, fill:{ color:"FFFFFF" } });
   slide.addShape(pres.shapes.RECTANGLE,         { x:1, y:1, w:0.08, h:1.5, fill:{ color:"0891B2" } });

   // 正确
   slide.addShape(pres.shapes.RECTANGLE, { x:1, y:1, w:3, h:1.5, fill:{ color:"FFFFFF" } });
   slide.addShape(pres.shapes.RECTANGLE, { x:1, y:1, w:0.08, h:1.5, fill:{ color:"0891B2" } });
   ```

## 快速参考

- **形状**：RECTANGLE、OVAL、LINE、ROUNDED_RECTANGLE
- **图表**：BAR、LINE、PIE、DOUGHNUT、SCATTER、BUBBLE、RADAR
- **版面**：LAYOUT_16x9（10"x5.625"）、LAYOUT_16x10、LAYOUT_4x3、LAYOUT_WIDE
- **对齐**："left"、"center"、"right"
- **图表数据标签**："outEnd"、"inEnd"、"center"
