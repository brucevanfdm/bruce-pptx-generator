# Custom Style Guide

> **Use this file only when NOT using a style preset.** If `default-style.md` (企业科技蓝) is active, this file is not needed — the preset already defines its own color palette, fonts, spacing, and page layouts.

This file covers two things needed together for any custom style:
1. **Design System** — color palette selection, fonts, style recipes, typography & spacing
2. **Slide Page Types** — 5 page type layouts, font hierarchies, content elements

---

## Part 1 — Design System

### Color Palette Reference

| # | Name | Colors | Style | Use Cases |
|---|------|--------|-------|-----------|
| 1 | Modern & Wellness | `#006d77` `#83c5be` `#edf6f9` `#ffddd2` `#e29578` | Fresh, soothing | Healthcare, counseling, skincare, yoga/spa |
| 2 | Business & Authority | `#2b2d42` `#8d99ae` `#edf2f4` `#ef233c` `#d90429` | Formal, classic | Annual reports, financial, corporate, government |
| 3 | Nature & Outdoors | `#606c38` `#283618` `#fefae0` `#dda15e` `#bc6c25` | Grounded, earthy | Outdoor gear, environmental, agriculture |
| 4 | Vintage & Academic | `#780000` `#c1121f` `#fdf0d5` `#003049` `#669bbc` | Classic, scholarly | Academic, history, museums, heritage brands |
| 5 | Soft & Creative | `#cdb4db` `#ffc8dd` `#ffafcc` `#bde0fe` `#a2d2ff` | Dreamy, candy-toned | Mother & baby, desserts, women's fashion |
| 6 | Bohemian | `#ccd5ae` `#e9edc9` `#fefae0` `#faedcd` `#d4a373` | Gentle, muted | Wedding, home decor, organic food |
| 7 | Vibrant & Tech | `#8ecae6` `#219ebc` `#023047` `#ffb703` `#fb8500` | High energy | Sports, startup pitches, youth education |
| 8 | Craft & Artisan | `#7f5539` `#a68a64` `#ede0d4` `#656d4a` `#414833` | Rustic | Coffee shops, handicrafts, bakery |
| 9 | Tech & Night | `#000814` `#001d3d` `#003566` `#ffc300` `#ffd60a` | Deep, luminous | Tech launches, luxury automobiles (dark mode) |
| 10 | Education & Charts | `#264653` `#2a9d8f` `#e9c46a` `#f4a261` `#e76f51` | Clear, logical | Statistical reports, education, market analysis |
| 11 | Forest & Eco | `#dad7cd` `#a3b18a` `#588157` `#3a5a40` `#344e41` | Monochrome, forest | Landscape, ESG reports, environmental |
| 12 | Elegant & Fashion | `#edafb8` `#f7e1d7` `#dedbd2` `#b0c4b1` `#4a5759` | Muted, Morandi | Haute couture, art galleries, beauty brands |
| 13 | Art & Food | `#335c67` `#fff3b0` `#e09f3e` `#9e2a2b` `#540b0e` | Rich, vintage-poster | Food documentaries, art exhibitions |
| 14 | Luxury & Mysterious | `#22223b` `#4a4e69` `#9a8c98` `#c9ada7` `#f2e9e4` | Cool, purple-toned | Jewelry, hotel, high-end consulting |
| 15 | Pure Tech Blue | `#03045e` `#0077b6` `#00b4d8` `#90e0ef` `#caf0f8` | Futuristic, clean | Cloud/AI, hospitals, clean energy |
| 16 | Coastal Coral | `#0081a7` `#00afb9` `#fdfcdc` `#fed9b7` `#f07167` | Refreshing, summery | Travel, beverage brands, ocean themes |
| 17 | Vibrant Orange Mint | `#ff9f1c` `#ffbf69` `#ffffff` `#cbf3f0` `#2ec4b6` | Bright, cheerful | Children's events, promotional, FMCG |
| 18 | Platinum White Gold | `#0a0a0a` `#0070F3` `#D4AF37` `#f5f5f5` `#ffffff` | Premium, professional | Agent products, fintech, luxury brands |

**Quick selection guide:**

| Presentation Type | Recommended Palette |
|------------------|---------------------|
| Finance / Data reports | 2 Business & Authority |
| Corporate / Business | 14 Luxury & Mysterious or 18 Platinum White Gold |
| Product intro / Marketing | 7 Vibrant & Tech or 17 Orange Mint |
| ESG / Environmental | 11 Forest & Eco |
| Healthcare | 1 Modern & Wellness |
| Tech / AI | 15 Pure Tech Blue or 9 Tech & Night |

### Color Rules

- Use **only** the chosen palette — do not create or modify colors
- No gradients — solid colors only
- No animations or transitions — all slides are static
- Transparency via the `transparency` property (0–100) only

### Font Reference

| Language | Default | Alternatives |
|----------|---------|--------------|
| Chinese | `Microsoft YaHei` | — |
| English | `Arial` | Georgia, Calibri, Cambria, Trebuchet MS |

**Recommended pairings:**

| Header | Body |
|--------|------|
| Georgia | Calibri |
| Arial Black | Arial |
| Cambria | Calibri |
| Trebuchet MS | Calibri |

- Body text: **never bold** — reserve bold for titles and headings only
- Mixed Chinese-English: Microsoft YaHei for Chinese segments, chosen English font for Latin

---

### Style Recipes

Choose one recipe for the entire presentation. Mixing recipes across slides looks inconsistent.

| Recipe | Corner Radius | Spacing | Best for |
|--------|--------------|---------|---------|
| **Sharp & Compact** | 0–0.05" | Tight | Data-dense, professional reports |
| **Soft & Balanced** | 0.08–0.12" | Moderate | Corporate, general business |
| **Rounded & Spacious** | 0.15–0.25" | Relaxed | Product intros, marketing |
| **Pill & Airy** | 0.3–0.5" | Open | Brand showcases, launch events |

**Component mapping:**

| Component | Sharp | Soft | Rounded | Pill |
|-----------|-------|------|---------|------|
| Button / Tag | 0 | 0.05 | 0.1 | 0.2 |
| Card / Container | 0.03 | 0.1 | 0.2 | 0.3 |
| Image Container | 0 | 0.08 | 0.15 | 0.25 |
| Badge | 0.02 | 0.05 | 0.08 | 0.15 |

**Rule**: outer container radius ≥ inner element radius. Never the reverse.

```javascript
// Sharp style card
slide.addShape("rect", { x:0.5, y:1, w:4, h:2.5,
  fill: { color: "F5F5F5" }, rectRadius: 0.03 });

// Pill style button (height 0.4" → rectRadius 0.2 = perfect pill)
slide.addShape("rect", { x:3, y:4, w:2, h:0.4,
  fill: { color: "4A90D9" }, rectRadius: 0.2 });
```

### Typography Scale

| Usage | Size (pt) |
|-------|-----------|
| Annotations / Sources | 10–12 |
| Body / Description | 14–16 |
| Subtitle | 18–22 |
| Title | 28–36 |
| Large Title | 44–60 |
| Data Callout | 60–96 |

### Spacing Scale (10" × 5.625" slide)

| Usage | Inches |
|-------|--------|
| Icon-to-text gap | 0.08–0.15 |
| List item spacing | 0.15–0.25 |
| Card inner padding | 0.2–0.4 |
| Element group gap | 0.3–0.5 |
| Page safe margin | 0.4–0.6 |
| Major block gap | 0.5–0.8 |

---

## Part 2 — Slide Page Types

Classify **every slide** as exactly one of these 5 types.

### 1. Cover Page

**Use for**: Opening + tone setting. Content: big title, subtitle, date/presenter, strong visual.

**Layout options:**

```
Asymmetric Left-Right:        Center-Aligned:
|  Title & Subtitle  | Image |  |         [BG Image]        |
|  Description       |       |  |         MAIN TITLE        |
                                |         Subtitle           |
```

**Font hierarchy:**

| Element | Size | Notes |
|---------|------|-------|
| Main Title | 72–120pt | Largest, focal point |
| Subtitle | 28–40pt | Clearly smaller than title |
| Supporting Text | 18–24pt | Base size |
| Meta (date, name) | 14–18pt | Smallest |

Title must be 2–3× larger than subtitle. Never let adjacent text elements be within 20% of each other's size.

**Content elements:** Main Title (required) · Subtitle · Icons · Date/Event · Company logo · Presenter name

---

### 2. Table of Contents

**Use for**: Navigation + expectation setting (3–5 sections).

**Layout options:**

```
Numbered Vertical List:       Two-Column Grid:
|  CONTENTS            |      |  01 Section  02 Section  |
|  01  Section One     |      |     Desc        Desc     |
|  02  Section Two     |      |  03 Section  04 Section  |

Sidebar Navigation:           Card-Based:
| ▌01 | Section One   |      | ┌──┐ ┌──┐ ┌──┐ ┌──┐    |
| ▌02 | Section Two   |      | │01│ │02│ │03│ │04│    |
| ▌03 | Section Three |      | └──┘ └──┘ └──┘ └──┘    |
```

**Font hierarchy:** TOC title 36–44pt · Section number 28–36pt · Section title 20–28pt · Description 14–16pt

**Decision guide:** 3 sections → vertical list; 4–6 → grid or compact; 7+ → multi-column. **Page badge: MANDATORY.**

---

### 3. Section Divider

**Use for**: Clear transitions between major parts. Content: section number + title + optional 1–2 line intro.

**Layout options:**

```
Bold Center:            Left-Aligned Accent:     Split Background:
|       02         |   | ████ | 02             | | ██████ | TITLE   |
|  SECTION TITLE   |   | ████ | SECTION TITLE  | | ██ 02  |         |
|  Optional intro  |   | ████ | Optional intro | | ██████ |         |
```

**Font hierarchy:** Section number 72–120pt · Section title 36–48pt · Intro text 16–20pt

**Rules:** Same divider layout across all dividers in one deck. Visually distinct from content slides (different background, more whitespace). **Page badge: MANDATORY.**

---

### 4. Content Page

Pick one subtype per slide — drives the entire layout.

**Subtypes:**

| Subtype | Layout sketch | Notes |
|---------|--------------|-------|
| Text | Title + bullets/paragraphs | Always add icons or shapes — never plain text only |
| Mixed Media | Two-column: text left, image right | |
| Data Visualization | Chart + takeaways + source | Must include data source |
| Comparison | Side-by-side columns or cards | A vs B, pros/cons |
| Timeline / Process | Numbered steps with arrows | |
| Image Showcase | Hero image or gallery, caption | |

**Font hierarchy:** Title 36–44pt · Section header 20–24pt · Body 14–16pt · Caption/source 10–12pt · Stat callout 60–72pt

**Rules:**
- Left-align all body text and bullets — never center paragraphs
- Title must be 36pt+ to contrast with 14–16pt body
- Every content slide needs at least one non-text visual element
- 0.5" minimum margins, 0.3–0.5" between content blocks
- Each slide should use a different layout from its neighbors
- **Page badge: MANDATORY**

**Additional layout patterns for variety:**
- Two-column (text left, illustration right)
- Icon + text rows (icon in colored circle, bold header, description below)
- 2×2 or 2×3 grid cards
- Half-bleed image with content overlay
- Large stat callouts (60–72pt numbers with small labels)
- Comparison columns (before/after, pros/cons)
- Timeline or process flow (numbered steps, arrows)

---

### 5. Summary / Closing Page

**Use for**: Wrap-up + action. Content: key takeaways, CTA/next steps, contact info, thank-you.

**Layout options:**

```
Key Takeaways:             CTA / Next Steps:
|  KEY TAKEAWAYS     |    |  NEXT STEPS           |
|  ✓  Point one      |    |  [1] Action item one  |
|  ✓  Point two      |    |  [2] Action item two  |
|  ✓  Point three    |    |  Contact: email       |

Thank You / Contact:       Split Recap:
|      THANK YOU     |    |  SUMMARY  |  NEXT STEPS  |
|  email@company.com |    |  * Point  |  Contact us  |
|  @handle           |    |  * Point  |  [QR Code]   |
```

**Font hierarchy:** Closing title 48–72pt · Takeaway / action item 18–24pt · Supporting text 14–16pt · Contact info 14–16pt

**Decision guide:** Many takeaways → list; Simple closing → centered thank-you; Action needed → CTA. Match energy of cover page. **Page badge: MANDATORY.**
