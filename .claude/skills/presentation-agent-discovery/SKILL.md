---
name: presentation-agent-discovery
description: Performs deep workspace scanning, schema parsing, and customer hypothesis elicitation to focus analysis.
risk: safe
date_added: "2026-07-19"
version: "1.0.0"
---

# Presentation Agent: Discovery & Hypothesis Elicitation

This skill manages the initial scoping phase of the analytical presentation creator workflow. It systematically maps all data schemas, notebook blocks, and presentation assets in the workspace, identifies potential business hypotheses, and interacts with the user to refine the scope of investigation.

## When to Use

Use this skill to scan a raw workspace and align on the exact analytical questions to answer before writing any analysis code or spawning modeling subagents.

## Ordered Steps

### Step 1: Scan Workspace Catalog
Scan the directory and document all files:
- Tabular data: `.csv`, `.xlsx`, `.sqlite`, `.json`
- Analytical code: `.ipynb`, `.py`
- Outlines/Previous presentations: `.ppt`, `.pptx`, `.txt`, `.md`

### Step 2: Read Schemas & Metadata
- For all discovered tabular datasets, run a lightweight inspection (first 10 rows, columns, data types, null counts, and simple summary stats).
- Parse existing `.ipynb` files to identify imported libraries (e.g., pandas, scikit-learn) and key variables.

### Step 3: Map Out Hypotheses
Formulate 3-5 strategic business questions that can be solved with the discovered data. For example:
- *Retention*: "Are monthly active users showing drop-offs in specific age cohorts?"
- *Monetization*: "What is the average transaction value difference between Mobile and Web users?"

### Step 4: User Elicitation
Ask the user:
> *"Here is the data catalog and schema structure I found. Based on this, I have drafted these potential business hypotheses to investigate. Are there any other key business questions or goals we should answer with this deck?"*

## Output Contract
Return a structured Markdown summary containing:
1. **Data Schema & File Registry**: Grid table listing files, row count, columns, and data quality issues.
2. **Scoping Hypotheses**: The list of agreed-upon analytical hypotheses to resolve in Phase 2.
