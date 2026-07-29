---
name: presentation-agent-rendering
description: Compiles slide outlines into single-page HTML slides with custom-coded, annotated Economist-style HTML/SVG charts.
risk: safe
date_added: "2026-07-19"
version: "1.0.0"
---

# Presentation Agent: Slide & Economist Chart Rendering

This skill compiles structured slide outlines into high-fidelity HTML/CSS files, combining McKinsey corporate layouts and aesthetics with the annotated, custom charts of *The Economist*.

## When to Use

Use this skill to convert consulting slide storyboards into beautiful, interactive, or static vector slide files.

## Visual Design Rules

### 1. McKinsey / BCG / Figma Aesthetics & Layouts
- **Typography & Scale**: Use a clean, premium sans-serif hierarchy (like Apple's San Francisco, Inter, or Roboto) with generous leading (line-height `1.5` to `1.65`). Slide titles should use a lighter weight (e.g. `300` or `400`) to feel elegant and airy, while key numbers use bolder weights.
- **Vast Negative Space**: Use spacious paddings (minimum `48px` to `80px` page borders) and wide margins between layout elements. Slides must fit exactly in `16in x 9in` boundaries without clipping.
- **Figma/Apple Minimalist Containers**: Use Figma-style sleek, minimal layouts. Soft, premium aesthetics:
  - Slide backgrounds: Clean white (`#ffffff`) or Apple's minimalist light grey (`#f5f5f7`).
  - Key Takeaway panels: Flat, premium minimalist panels (`#f0f4f8` or `#e8e8ed`) with modern soft rounded corners (`16px` to `24px` border-radius).
  - Primary text color: Sleek dark grey (like Apple's `#1d1d1f`) or Figma charcoal (`#333333`).
- Use a single visual focus per slide (e.g., one huge chart container, left-aligned text blocks).
- **Information Density & Text Constraints**: Be as descriptive as possible with the text on the slide, but **strictly ensure there is absolutely no text overflow**. Adjust font sizes, line heights, or paddings dynamically to accommodate descriptive text within bounds.

### 2. McKinsey/Economist Hybrid Charts (Charts Only)
- **Signature Accent Line**: A sleek minimalist Apple-style accent line or Figma vibrant gradient banner (4px height) at the top of the chart card.
- **Chart Palette (Apple/Figma/Minimalist)**: Combine McKinsey/Economist data storytelling with a vibrant, modern minimalist palette. Use iOS Blue (`#007aff`), Figma Purple (`#A259FF`), vibrant clean accents (`#34c759`), and minimalist neutral greys (`#86868b`) for secondary/inactive data.
- **Annotated Data Points**: Overlay SVG path arrows or callout text boxes directly on top of coordinates to highlight spikes or drops.
- **Direct Axis Labeling**: Write text labels next to line ends or bar ends rather than placing them in separate color legends.
- **Chart Scaling**: The chart must **not stick to just one corner**. The chart must fill the entire container completely and proportionally. **It must not look stretched**. Use responsive viewBox scaling (`preserveAspectRatio="xMidYMid meet"`) or dynamic coordinate generation to ensure the chart occupies all available space within the `.economist-chart-card` without distortion.
- **Clean Gridlines**: Subtle horizontal gridlines only (`#e5e7eb`); hide vertical grids.
- **Cohesive Fonts**: Arial/Helvetica for chart headers; Arial/Inter for data values.


### 3. Supporting Slide Layouts
- **Title Slide layout**: A bold, minimalist Figma/Apple-inspired design. A solid sleek dark background (`#1d1d1f` or deep minimal tone) with clean white typography, or a clean white background with sleek dark grey text. Massive font sizes for the title, vertically centered or strongly left-aligned. Subtitle and author/date at the bottom.
- **Agenda / Index layout**: Clean, numbered lists with vast negative space and large typography to outline the deck's flow.
- **Conclusion layout**: A single-column or simplified grid layout for high-level textual takeaways without a chart. Focus on action-oriented text.

## Ordered Steps

### Step 1: Create Slide Markup
- Parse the slide `Type` from the storyboard to determine the appropriate HTML class layout (e.g., `.slide-title`, `.slide-agenda`, `.slide-content`, `.slide-conclusion`).
- Apply a zero-dependency HTML layout utilizing flexbox or CSS grid.
- **McKinsey/BCG/Figma Slide Layout**: Structure each content slide as a 2-column grid:
  - **Left Column**: The `.economist-chart-card` container (enforcing 60-65% width share) containing the title, subtitle, SVG canvas, and annotations. Keep this card clean and minimalist with transparent/white backgrounds and render McKinsey/Economist-style charts inside it.
  - **Right Column**: The `.key-takeaways-panel` container (35-40% width share), styled as a flat premium minimalist panel (e.g. `#f5f5f7`), soft rounded corners (`16px` to `24px` border-radius), zero box-shadows, zero borders, and left-aligned text with Inter/San Francisco fonts and bullet points starting with bold tags (`<strong>`) for immediate executive readability.
- **Footer Section**: Place absolute-positioned attribution footnotes (`.slide-attribution`) and slide page counts at the bottom of the slide.

- Integrate modern CSS transitions for fade-in animations on page load.
- **Print Optimization & Truncation Fixes**: Enforce `@media print` and `@page` styles inside the HTML markup. 
  - Size must be explicitly set to `1920px 1080px` (standard 16:9 widescreen layout) using `@page { size: 1920px 1080px; margin: 0; }` to eliminate whitespace.
  - Under `@media print`, reset the body, `.presentation-container`, and `.slides-wrapper` to `display: block !important; overflow: visible !important; width: 100% !important; height: auto !important; transform: none !important; margin: 0 !important; padding: 0 !important;`.
  - Set `.slide` to `display: grid !important; page-break-after: always !important; break-after: page !important; width: 1920px !important; height: 1080px !important; overflow: hidden !important; box-sizing: border-box !important;` to completely prevent page truncation, page overflows, or scaling issues. Avoid using relative viewport units (`100vh`, `100vw`) or inches (`in`) in print media styles, as they can cause text/chart truncation or leave whitespace due to mismatch with absolute pixel boundaries.
  - Hide all navigation elements during print.




### Step 2: Code Custom Charts
- Translate raw data numbers into inline CSS bar ratios or SVG coordinate points.
- Code custom annotations (such as `<svg>` dashes, text callouts, or highlight bands).
- **Absolute SVG Heights**: Never set inline SVG heights or chart heights to relative percentages (`100%`). Always specify absolute heights (e.g., `height="240"` or `height: 240px !important;`) directly on the SVG element. This prevents flexbox/grid layout collapses or chart truncation when rendering to vector formats (PDF/PPTX).
- **SVG Canvas Fitting & ViewBox Padding**: Ensure that the SVG coordinate space has at least `30px` to `40px` of padding/margins on all four sides inside the `viewBox` coordinate system. For example, if the viewBox is `0 0 450 300`, all shapes, axes, text labels, and callout annotations must lie strictly within `x=[30, 420]` and `y=[30, 270]` boundaries. This prevents axes text, titles, or highlight arrows from clipping at the SVG canvas boundaries.
- **Strict Left Alignment**: Enforce left-alignment on all custom charts. On all inline `<svg>` elements, explicitly set the attribute `preserveAspectRatio="xMinYMin meet"` and apply `margin-left: 0;` in styles to prevent the browser or print engine from center-aligning the visual graphics.
- **Parent Overflow Settings**: Enforce `overflow: visible;` on `.chart-content` to allow minor annotation overflows to render fully, while keeping the parent `.economist-chart-card` spacious enough to pad the entire graphic without layout shifts.




### Step 3: Add Navigation Scripting
- Include keys (arrows, space) and mouse/swipe events to slide forward/backward.
- Add toggleable sidebar for notes.

### Step 4: Add Supporting Data Appendix
- **Appendix Generation**: For all charts generated in the presentation, append an "Appendix" section at the end of the slide deck. This section must contain all the supporting data (in tables or raw JSON formats) necessary to exactly recreate the charts. This allows stakeholders to audit the precise metrics used.

### Step 5: Export to Target Format
- Output the HTML deck file (`presentation.html`) directly inside the current run folder: `outputs/run_YYYYMMDD_HHMMSS/presentation.html`.
- **Compile to PDF (Primary Deliverable)**: Compile the HTML slides to a print-ready vector PDF using Google Chrome's headless print command on Windows. You MUST use `Start-Process -Wait` and absolute paths to ensure it doesn't fail silently. Include `--window-size=1920,1080` to enforce a 16:9 aspect ratio and eliminate whitespace at the edges:
  ```powershell
  $htmlPath = (Resolve-Path "outputs\run_YYYYMMDD_HHMMSS\presentation.html").Path
  $pdfPath = (Join-Path (Get-Location).Path "outputs\run_YYYYMMDD_HHMMSS\presentation.pdf")
  $arguments = "--headless=new", "--disable-gpu", "--window-size=1920,1080", "--print-to-pdf=`"$pdfPath`"", "--no-margins", "--include-background-colors", "`"$htmlPath`""
  Start-Process -FilePath "C:\Program Files\Google\Chrome\Application\chrome.exe" -ArgumentList $arguments -Wait -NoNewWindow
  ```
- **Compile to PPTX**: If PPTX is explicitly preferred, translate the slide coordinates and layout shapes into XML PPTX format via python script.

### Step 5: Visual Validation & Self-Correction Loop
Immediately after compiling `presentation.pdf`, the agent must visually check the final PDF slides. **Do not run the visual check on the raw HTML.** The PDF compilation step itself introduces scaling shifts, print margins, font replacements, and text-wrapping breaks that differ from browser views.
- **Conversion to Image**: Convert the pages of the compiled `presentation.pdf` directly into high-resolution images (PNG) using `pdf2image` or Chrome headless rendering.
- **Multimodal Visual Audit**: Programmatically inspect or visually review these compiled slide images verifying these **10 Visual Correctness Criteria**:
  1. **Text Overlap Audit**: Ensure no text labels (such as SVG numeric markers, axis coordinates, or legend annotations) intersect or collide with adjacent text nodes or gridlines.
  2. **Container Boundaries Check**: Confirm that no chart, line, or bar visual extends outside the bounding border of the `.economist-chart-card` card canvas.
  3. **Responsive Grid Splits**: Verify that the slide forms a balanced 2-column layout (60% left visual, 40% right textual takeaways) with distinct, clear horizontal gutter margins.
  4. **Header Alignment**: Ensure the signature top border (sleek accent line or gradient banner) aligns perfectly with the slide title baseline, with zero vertical gap offsets.
  5. **Direct Label Proximity**: Verify that axis data labels are positioned directly adjacent to line endpoints or bar ends to allow immediate correlation without separate color legends.
  6. **Background Contrast Check**: Confirm all text colors satisfy contrast ratios against background fills (e.g., dark charcoal `#0f172a` text on off-white `#f8f9fa` slides, and clean white text on the dark cover slide).
  7. **Bullet Lead-In Styling**: Ensure takeaway lists contain bold headers (`<strong>`) for executive scanning, with clean line-height margins.
  8. **Footnote Positioning**: Verify that absolute-positioned footnotes (`.slide-attribution`) rest at the bottom left within safe margins (min 40px padding from the page edge).
  9. **Spike Callout Proximity**: Ensure that highlight annotations (like failed-login spike arrows or value labels) point directly at the anomalous data node without overlapping the chart lines themselves.
  10. **Bubble Chart Transparency**: In bubble metrics, verify that bubbles use opacity transparency (`opacity="0.8"`) to keep smaller underlying clusters fully visible and readable.
**Self-Correction Loop**: If any of these 10 visual checks fail on the compiled PDF page images, log the compilation defect (e.g., "slide 3 line-wrap overlap"), feed it back into the generator script to adjust layout bounds or coordinates, re-render, and re-print. Repeat this correction loop up to a maximum of 3 times.



## Output Contract
- Path to the compiled vector PDF slides under `outputs/run_YYYYMMDD_HHMMSS/presentation.pdf`.

- Path to the compiled HTML presentation under `outputs/run_YYYYMMDD_HHMMSS/presentation.html`.
- Embedding verification checklist.


