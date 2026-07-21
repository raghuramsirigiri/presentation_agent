---
name: notebook-presentation-creator
description: Automatically scans workspaces, performs impactful analytical updates with a notebook trail, synthesizes insights like a McKinsey/BCG consultant, and compiles slide decks with hybrid McKinsey/Economist-style HTML charts.
risk: safe
date_added: "2026-07-19"
version: "1.0.1"
---

# Notebook Presentation Creator

This is the orchestrator skill that coordinates a multi-step analytical and presentation workflow. It delegates specific tasks to specialized subagents and sub-skills to scan a directory, perform additional calculations, write clean Jupyter Notebook trails, draft BCG/McKinsey-style slides, and compile them into stunning McKinsey/Economist hybrid HTML/PDF slide decks.

## When to Use This Skill

Use this skill when you want to convert raw datasets and script directories into professional, highly polished management presentations.

## Subagent & Sub-Skill Routing Table

The orchestrator coordinates the process by routing to these specialized sub-skills:

| Phase | Task | Sub-Skill Folder |
|-------|------|------------------|
| **Phase 1 & 2** | Discovery & Scoping | [presentation-agent-discovery](file:///C:/Users/raghu/Documents/AG%20Projects/presentation_agent/.claude/skills/presentation-agent-discovery/SKILL.md) |
| **Phase 3 & 4** | Execution Trail | [presentation-agent-execution](file:///C:/Users/raghu/Documents/AG%20Projects/presentation_agent/.claude/skills/presentation-agent-execution/SKILL.md) |
| **Phase 5** | McKinsey/BCG Narrative | [presentation-agent-synthesis](file:///C:/Users/raghu/Documents/AG%20Projects/presentation_agent/.claude/skills/presentation-agent-synthesis/SKILL.md) |
| **Phase 6 & 7** | Slide/Chart Render | [presentation-agent-rendering](file:///C:/Users/raghu/Documents/AG%20Projects/presentation_agent/.claude/skills/presentation-agent-rendering/SKILL.md) |

---

## Core Process Workflow

### Step 1: Workspace Discovery & Dynamic Run Directory Creation
- Trigger **`presentation-agent-discovery`**.
- Scan all file formats (`.csv`, `.xlsx`, `.ipynb`, `.py`, `.ppt`, `.pptx`).
- Create a new timestamped output directory inside the workspace: `outputs/run_YYYYMMDD_HHMMSS/` (e.g., `outputs/run_20260719_013414/`).
- Present schema information to the user and prompt them with:
  > *"Are there any specific, important business questions or hypotheses you want this analysis to answer?"*
- Log initial scoping parameters and bind them to the timestamped run directory.

### Step 2: Planning & Iterative Subagent Execution Loop
- Trigger **`presentation-agent-execution`**.
- Divide the approved questions into baseline analytical modules.
- **Iterative Diagnostic Loop**: Programmatically run the baseline notebooks, analyze the results for statistical anomalies (spikes, margin leaks, cohort decay) using dynamically calculated metrics (IQR, Z-scores, percentiles, Pareto cuts) with zero hardcoded thresholds, and dynamically spawn subsequent subagents to build deep-dive notebooks investigating the root causes (up to 3 levels of depth).
- Compile a complete, hierarchical lineage trail log of all executed notebooks.


### Step 3: McKinsey/BCG Insight Synthesis
- Trigger **`presentation-agent-synthesis`**.
- Filter out raw code details; structure the slides top-down using the Minto Pyramid Principle.
- Design active, bold headlines and map the narrative to a strict **2-column McKinsey/BCG slide grid**:
  - **Left Column**: Visual chart or data table.
  - **Right Column**: Structured Key Takeaways panel with bold leading-word bullets.
- Write the storyboard outline file (`storyboard.md`) inside the active run directory.

### Step 4: McKinsey/Economist-Style Slide Rendering & Compilation (PDF/PPTX)
- Trigger **`presentation-agent-rendering`**.
- Compile slide structures into print-ready, minimalist, 16:9 landscape HTML templates implementing the 2-column grid layout (Left: Chart, Right: Bullet list) and bottom attribution footers.
- Generate custom-coded HTML/CSS/SVG charts using a McKinsey-aligned palette (deep blues, high contrast professional neutrals), direct value labeling, and detail annotations (arrows, highlight callouts).
- Export slide files directly into the active run directory as `presentation.html`, then trigger a headless compile step (e.g. via Chrome on Windows) to output a vector-perfect PDF (`presentation.pdf`) or PPTX (`presentation.pptx`) as the primary final deliverable.
- **Post-Generation Validation & Correction**: Run visual check validations (structural grid checks, vector bounds audits, and placeholder scanning). If any defects are discovered, automatically loop back to re-generate the visual structures, continuing until the slide outputs achieve absolute correctness (up to 3 correction iterations).


---

## Output Contract
Upon completion, the orchestrator returns:
1. **Timestamped Directory Path**: e.g., `outputs/run_YYYYMMDD_HHMMSS/`.
2. **Summary** of the workspace state and data context.
3. **Lineage Audit Trail Table** listing all baseline and deep-dive notebooks with their trigger conditions.
4. **Storyboard Outline** showing slide topics, active titles, and 2-column text and chart specifications.
5. **Final Compiled Presentation Slide File**: The vector PDF (`outputs/run_YYYYMMDD_HHMMSS/presentation.pdf`) or PPTX (`outputs/run_YYYYMMDD_HHMMSS/presentation.pptx`) as the primary product.



