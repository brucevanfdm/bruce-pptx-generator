# QA 检查清单与常见错误

API 层面的陷阱（十六进制颜色格式、复用选项对象等），请参阅 [pptxgenjs.md](pptxgenjs.md#common-pitfalls)。

## 编译前代码审查（第 5.5 步）

在编译之前执行此步骤。由于无法直接看到渲染结果，必须在代码阶段提前发现布局问题。

逐一检查每个幻灯片 JS 文件，核对以下每一项。**将所有发现的问题写下来——不要悄悄修复。**

### 0. 内容富足度检查（精装标准）

在检查布局之前，先检查内容是否达到「精装房」标准。以下任一问题存在，都必须返回修改，不得进入编译。

- [ ] **数据/统计检查**：每个核心论点是否有至少一个数字、比例、时间范围或行业数据支撑？
  - 例："覆盖 1.18 亿空巢老人"、"慢病随访断档率 > 60%"、"准确率 > 95%"
  - 反例："很多医院数据保存时间很短" ← 无数据，不合格
- [ ] **Tagline 检查**：每张卡片/模块是否有一句 12–20 字的定位语，说明能解决什么问题？
  - 反例：仅有"生物识别安全" ← 无 tagline，不合格
- [ ] **Bullet 前缀检查**：要点列表是否使用小方块/圆点/编号前缀，而非纯文本堆叠？
- [ ] **非文字视觉检查**：除苹果极简风格外，每张内容页是否至少包含一种 SVG 图标/流程图/进度环/数据表格/对比矩阵/KPI 卡？
  - 纯文字列表页（只有标题+bullet）视为毛坯房，必须添加至少一个视觉元素
  - 同时检查：**单页是否出现两种大型图形组件**（进度环 + 矩阵、流程图 + 金字塔 = 溢出风险极高），若有则拆分或移除一个
- [ ] **底部说明检查**：每个核心模块底部是否有 1–2 行补充说明或价值洞察？
- [ ] **封面检查**：封面页是否包含装饰性几何图形、右侧能力矩阵或其他非文字视觉元素？

**问题报告格式示例：**
```
slide-04.js: 卡片仅有 title+desc，无 tagline、无 bullet 前缀、无底部说明 → 升级为 addHuaweiRichCard
slide-05.js: 纯文字内容页，无任何 SVG 图标/流程图/数据卡 → 添加至少一个非文字视觉元素
```

### 0.5 精装修复矩阵

发现问题后，对照此矩阵执行**具体的升级动作**，而非泛泛地"修改内容"：

| 失败症状 | 根因 | 升级动作 |
|---------|------|---------|
| 卡片只有 title + desc，无 tagline、无 bullet | 使用了基础组件 | 替换为对应风格的 Rich Card：`addHuaweiRichCard` / `addMcKinseyRichCard` / `addAppleRichCard` / `addPitchRichCard` / `addDarkRichCard` / `addDataRichCard` |
| 内容页无任何视觉元素，只有文字列表 | 缺少非文字视觉 | 按复杂度**从低到高**选择，优先低复杂度：① 给每条 bullet 加彩色前缀几何图形（OVAL/RECTANGLE 0.1"，颜色用 `theme.secondary` 或 `theme.accent`）② SVG 图标（`svgToBase64`）③ KPI 数据卡 ④ `makeProcessNode` 流程图（仅当内容本身是流程时）⑤ 对比矩阵（仅当需要逐列对比时）。**不要默认添加进度环（`makeProgressRing`）或金字塔**——它们占用大量垂直空间，文字挤不下时 PptxGenJS 静默截断。 |
| 论点无数字支撑（"大幅提升"等） | 数据缺位 | ① 替换为具体数字（优先用用户提供的数据）② 使用行业基准并加注「参考估算」③ 不允许保留模糊表述 |
| 无 tagline（只有标题，无定位句） | 漏写 tagline | 在标题下方/卡片内补加 12–20 字精准定位语，说明「解决什么问题」或「带来什么价值」 |
| bullet 无视觉前缀（纯文本堆叠） | 缺少前缀元素 | 在每条 bullet 前加小方块 `pres.shapes.RECTANGLE`（宽高 0.1"）或圆点 `OVAL`，颜色用 `theme.secondary` 或 `theme.accent` |
| 卡片/模块底部无说明区 | 漏写 detail 参数 | 补充 `detail` 参数，内容为 1–2 行洞察或行动建议；若 Rich Card 函数已有 `detail` 参数，填入即可 |
| 封面无装饰元素（只有标题+日期） | 封面毛坯 | 添加 `createRichCover`（推荐）或手动在封面右侧加几何装饰色块 + 能力标签卡 |
| 连续 3 张以上相同布局 | 布局单调 | 在第 3 张同类型幻灯片后插入图表页、KPI 页或流程图页，打破视觉节奏 |

### 0.8 骨架完整性检查（Master / Placeholder / Section / Appendix）

在进入布局检查前，先确认 deck skeleton 没有塌：

- [ ] **Master 检查**：重复 chrome（logo、页眉、页脚、页码轨道、固定免责声明）是否优先放在 master，而不是每页重复手绘？
- [ ] **Placeholder 检查**：标题区、正文区、图表区、表格区等稳定槽位，是否优先使用 placeholder 而非每页重新算坐标？
- [ ] **Section 检查**：除封面/目录外，每张章节分隔页、内容页、附录页、总结页是否都带有正确的 `sectionTitle`？
- [ ] **Appendix 检查**：超出安全密度的长表格，是否已经转入 appendix，并启用 `autoPage` 与重复表头？

**问题报告格式示例：**

```text
compile.js: section "解决方案" 未通过 pres.addSection() 注册 → ADD SECTION
slide-08.js: 重复绘制页眉和页码条，实际应放进 CONTENT_MASTER → MOVE TO MASTER
slide-10.js: 42 行明细表仍放在内容页，字号降到 9pt → MOVE TO APPENDIX + ENABLE AUTOPAGE
```

### 1. 边界检查

幻灯片画布尺寸：**宽 10 英寸 × 高 5.625 英寸**。每个元素必须满足：

```
x >= 0  AND  x + w <= 10
y >= 0  AND  y + h <= 5.625
```

常见陷阱：
- 形状 `x:0.5, w:9.8` → 右边缘 = 10.3 ✗ 溢出
- 文本 `y:5.0, h:0.8` → 底部 = 5.8 ✗ 溢出
- 页码标记 `x:9.3, w:0.4` → 右边缘 = 9.7 ✓

**标记所有 `x+w > 10` 或 `y+h > 5.625` 的元素。**

### 1.5 文字溢出估算检查（防截断）

> PptxGenJS **不报错、不换行到下一页**，文字超出 `h` 直接静默截断。每个 body 文本框写入前必须估算内容是否放得下。

**估算公式**（字号 12pt，lineSpacingMultiple 1.3）：

```
每行高度 ≈ 0.205"
中文：每行约 20–22 字 | 英文：每行约 40–44 字
估算行数 = ceil(字数 / 每行字数)
需要高度 = 估算行数 × 0.205"
```

| 分配高度 | 可容纳中文行数 | 最大字符数参考 |
|----------|--------------|--------------|
| 0.5" | 2 行 | ≤ 44 字 |
| 0.72" | 3 行 | ≤ 66 字 |
| 0.9" | 4 行 | ≤ 88 字 |
| 1.2" | 5–6 行 | ≤ 130 字 |
| 1.6" | 7–8 行 | ≤ 176 字 |

**高风险区（重点检查）：**

- KPI 卡的标签区（`h ≈ 0.35–0.4"`）— 超过 12 字必须截短
- 流程节点说明（`h ≈ 0.5–0.7"`）— 超过 40 字需要缩小字号或减少文字
- 进度环 / 金字塔层 旁边的说明文字（剩余宽度可能不足）— 写入前先计算剩余空间
- 任何卡片 body 区（`h = cardH - header_h`）— 动态计算高度时必须同步估算文字量

**修复协议**：估算超出时，**优先裁减文字**（删至估算范围内），其次调大 `h`（但不能超过 `y:5.0`），最后才考虑缩小字号至 11pt（此时每行高约 0.188"）。

### 2. 重叠检查

对每张幻灯片，检查是否存在非预期的重叠。两个元素发生重叠的条件：

```
A.x < B.x+B.w  AND  A.x+A.w > B.x
AND
A.y < B.y+B.h  AND  A.y+A.h > B.y
```

有意为之的重叠（如背景形状上的文本）是允许的。以下非预期情况需标记：
- 两个文本框位置相近，会相互遮挡
- 某形状覆盖了不应被遮挡的文本元素
- 正文内容超过 `y:5.0`（页码标记位于 `y:5.1`）

### 3. 背景一致性

相同类型的幻灯片必须使用完全一致的背景：

| 幻灯片类型 | 预期背景 |
|------------|----------|
| 封面 | 整套 PPT 统一使用同一选择 |
| 目录 | 与封面一致，或使用指定变体 |
| 章节分隔页 | **所有分隔页使用相同值** |
| 内容页 | **所有内容页必须完全一致** |
| 总结页 | 与封面或指定结尾风格保持一致 |

常见问题：某内容页使用 `theme.bg`，另一页使用 `"FFFFFF"` —— 当前视觉效果相同，但一旦 theme 变更就会出错。

**修复方式**：在 `compile.js` 中统一定义背景，再传入各页：

```javascript
const backgrounds = {
  cover:   theme.bg,
  toc:     theme.bg,
  divider: "EEF6FF",
  content: "FFFFFF",   // 所有内容页必须使用这个完全相同的字符串
  appendix:"F8FAFC",
  summary: theme.bg,
};
```

### 3.5 Master / Placeholder 合规

对使用生成路径的 deck，额外检查：

- `compile.js` 是否先定义 `defineSlideMaster()`，再开始添加 slide
- slide 文件是否通过 `pres.addSlide({ masterName, sectionTitle })` 显式使用 master
- 标题、正文、图表、表格这些稳定区域，是否优先通过 `placeholder` 填充
- 是否仍有大量“明明固定却每页重复手画”的元素留在 slide 文件里

常见问题：

- 在 master 已可覆盖页眉/页脚时，slide 文件仍重复绘制
- 同一类内容页，有的用 placeholder，有的完全手工定位，导致难以统一维护
- 使用了 placeholder 但命名漂移，例如同一语义槽位在不同 slide 分别叫 `body`、`contentBody`、`mainText`

### 4. 字体合规检查

扫描每一个 `fontFace` 值，应全部为：
- `"Microsoft YaHei"` — 中文或中英混排内容
- 指定的英文字体（`"Arial"`、`"Georgia"` 等）

标记任何不在预期范围内的字体名称。

### 5. 颜色合规检查

- 所有颜色应来自 `theme.*`
- 允许例外：`"FFFFFF"`（白色）、`"000000"`（黑色）
- **任何地方不得使用 `"#"` 前缀** — `"#FF0000"` 会导致文件损坏
- 不得使用 8 位十六进制字符串来编码透明度 — 请使用 `opacity` 属性

### 6. 页码标记

除封面外，每张幻灯片都必须有页码标记。检查：
- 标记是否存在
- 标记显示的编号是否按顺序正确
- 位置：**以当前预设文件中 `addPageBadge` 的实际坐标为准**（各预设实现略有差异）。SKILL.md 中列出的是参考规格，不作为 QA 判断依据。
  - 华为 / Pitch Deck：`x:9.1, y:5.15, w:0.6, h:0.35`（胶囊形）
  - Dark Tech：`x:9.3, y:5.1, w:0.4, h:0.4`（圆形）
  - McKinsey：`x:9.2, y:5.1, w:0.55, h:0.35`
  - 数据分析：`x:9.3, y:5.2, w:0.4, h:0.28`
  - 苹果极简：见预设文件

### 6.5 Section 一致性

检查 deck 的章节结构是否一致：

- `pres.addSection({ title })` 中注册的章节数量，是否与 TOC 和 Section Divider 数量匹配
- 每张 `Section Divider` / `Content` / `Appendix` / `Summary` 页的 `sectionTitle` 是否指向已注册 section
- TOC 中的章节标题、章节页标题、section title 是否完全一致，不能出现“目录叫解决方案、section 叫方案总览”这种漂移

**问题报告格式示例：**

```text
compile.js: TOC 有 4 个章节，但只注册了 3 个 pres.addSection() → SECTION MISMATCH
slide-06.js: sectionTitle = "落地计划", 但已注册 section 为 "实施计划" → TITLE DRIFT
```

### 7. 标题结构

对每张内容页 / 目录页 / 总结页：
- 标题 `y` 位置在所有内容页中保持一致（例如 `y:0.22`）
- 标题使用 `bold: true` 和 `color: theme.primary`
- 若风格要求带强调条（参见当前 preset 的标题组件），该线条应位于标题下方

### 8. 跨页一致性矩阵

完成单页检查后，进行一次跨页整体审查。构建如下表格：

| 幻灯片 | 类型 | Master | Section | 标题 y | fontSize | 内容起始 y | 背景 |
|--------|------|--------|---------|--------|----------|------------|------|
| 01 | cover | `COVER_MASTER` | — | — | — | — | `theme.bg` |
| 02 | toc | `TOC_MASTER` | — | 0.22 | 28 | 0.9 | `theme.bg` |
| 03 | divider | `SECTION_MASTER` | 市场机会 | — | — | — | `EEF6FF` |
| 04 | content | `CONTENT_MASTER` | 市场机会 | 0.22 | 28 | 1.05 | `FFFFFF` |
| 05 | content | `CONTENT_MASTER` | **解决方案** | **0.30** | **26** | 1.05 | `FFFFFF` ← **标记：y 和 fontSize 不一致** |

标记同类型幻灯片中上述值有差异的情况，并额外标记：

- 同类型页却使用了不同 master
- 本应属于某 section 的页没有 section
- appendix 页误用了 content master

### 9. SVG / 图片元素尺寸检查

对所有 `slide.addImage({ data: ..., x, y, w, h })` 调用（包括 SVG 图形和 react-icons 图标），检查：

- `x + w ≤ 10` 且 `y + h ≤ 5.625`（同普通元素）
- SVG 生成函数的 `w`/`h` 参数单位为**像素（px）**，`addImage` 的 `w`/`h` 单位为**英寸（in）** — 二者无需匹配，SVG 会自动缩放
- 推荐尺寸对应关系（供参考）：
  - 全宽图表/瀑布图：`w: 9.2`
  - 半宽图表 + 右侧文字：`w: 5.8`
  - 进度环（单个）：`w: 1.2–1.5, h: 1.2–1.5`
  - 时间轴（底部跨页）：`w: 9.2, h: 1.5–2.0`
  - 漏斗/金字塔：`w: 3.5–5.0, h: 3.0–3.8`
  - 2×2 矩阵/SWOT 各象限由代码控制，无需检查 addImage

**异步图标预生成检查：**
- `icon-utils.js` 存在于 `slides/` 目录
- `compile.js` 顶部所有 `iconToBase64Png` 调用均在 `for` 循环之前完成
- 无任何 `await` 出现在 `createSlide()` 函数体内

**Appendix 表格分页检查：**

- 明细表是否启用 `autoPage: true`
- 是否启用 `autoPageRepeatHeader: true`
- 多列表头时是否指定 `autoPageHeaderRows`
- 自动分页后的续页是否仍保留 appendix 标题语境和 section 归属

### 问题报告格式

```
slide-04.js: shape x:0.5 w:9.8 → right=10.3 → OVERFLOW, change w to 9.5
slide-05.js: background "FFFFFF" but other content slides use theme.bg → INCONSISTENCY
slide-06.js: page badge missing → ADD BADGE
slide-07.js: title y:0.30 but others are y:0.22 → TITLE DRIFT
```

在编译前修复所有已标记的问题。

## 编译后 QA

**默认假设存在问题。你的任务是找出它们。**

第一次渲染几乎不会完全正确。将 QA 作为 bug 排查过程来对待，而非确认步骤。

### 内容提取

前提：确认已安装 markitdown（`pip install markitdown`）。若未安装，退而用 PowerPoint 手动逐页核对内容。

```shell
python -m markitdown output.pptx
```

检查：内容缺失、顺序错误、文本截断。

### 占位符残留检查

```shell
# bash / zsh
python -m markitdown output.pptx | grep -iE "xxxx|lorem|ipsum|placeholder|TODO"

# PowerShell
python -m markitdown output.pptx | Select-String -Pattern "xxxx|lorem|ipsum|placeholder|TODO" -CaseSensitive:$false
```

如果有返回结果，修复后才能宣告完成。

若使用了 master placeholder，额外检查：

- `(title placeholder)`、`(body placeholder)` 等默认占位文字是否仍出现在导出结果中
- appendix 自动分页续页中，是否出现未填充的 placeholder 文本

### 验证循环

1. 编译 → 使用 markitdown 提取 → 审查内容
2. **列出发现的问题** — 如果没有发现，再更仔细地检查一遍
3. 修复源 JS 文件 → 重新编译
4. 重新验证受影响的幻灯片 — 一处修复往往会引发另一处问题
5. 重复循环，直到完整检查一遍后不再出现新问题

**至少完成一次"修复并验证"循环后，才能宣告成功。**

## 常见错误汇总

### 布局与定位

- **溢出** — 始终验证 `x+w ≤ 10` 和 `y+h ≤ 5.625`
- **正文触及页码区域** — 正文内容必须在 `y:5.0` 前结束；页码标记位于 `y:5.1`
- **背景不一致** — 在 `compile.js` 中统一定义，再传入各页；不要在每张幻灯片中硬编码
- **文本框默认边距** — PptxGenJS 会添加内部内边距；需要精确对齐文本与形状时，设置 `margin: 0`
- **对比度不足** — 图标和文本都需要与背景有足够的对比度
- **大面积留白** — 使用图形布局组件（G1–G5）填充内容区域 `y:1.05–5.0`
- **固定元素重复绘制** — 明明可进入 master 的页眉、页脚、页码轨道，却在每页重复手写

### 内容与风格

- **布局重复** — 跨幻灯片变换布局类型；使用 workflow.md 中的图形布局选择器
- **正文居中** — 段落和列表应左对齐；只有标题和 KPI 数字才居中
- **字号对比弱** — 标题需要 28pt 以上，才能与 12–14pt 正文形成视觉区分
- **描述仅一个关键词** — 每项写 2–3 行完整句子，让客户无需主讲人也能理解
- **纯文字幻灯片** — **毛坯房**，必须添加 SVG 图标、流程图、数据卡、KPI 卡或对比矩阵等至少一种非文字视觉元素；避免仅有标题加项目符号列表

### PptxGenJS 正确性

- **十六进制颜色带 `"#"` 前缀** — 会导致文件损坏；始终使用 `"FF0000"` 而非 `"#FF0000"`
- **在十六进制字符串中编码透明度** — `"00000020"` 会损坏文件；请使用 `{ color: "000000", opacity: 0.12 }`
- **在 `createSlide()` 中使用 `async`** — `compile.js` 不会等待异步；始终使用同步写法
- **复用选项对象** — PptxGenJS 会就地修改对象；对于阴影等共享选项，使用工厂函数生成
- **未先注册 master / section 就直接 addSlide** — deck 结构会退化成一堆孤立页面
- **长表格未开启自动分页** — 内容会被静默截断，或被压缩到不可读
