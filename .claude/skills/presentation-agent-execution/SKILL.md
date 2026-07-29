---
name: presentation-agent-execution
description: Delegates analytical tasks to subagents to perform code operations and outputs a clean notebook trail.
risk: safe
date_added: "2026-07-19"
version: "1.0.0"
---

# Presentation Agent: Execution Trail & Subagent Coordination

This skill manages the execution phase where analytical questions are turned into programmatic steps, executed in parallel notebooks, and logged as an audit trail.

## When to Use

Use this skill once the scoping hypotheses have been agreed upon with the user and you need to run mathematical, modeling, or statistical code blocks.

## Ordered Steps

### Step 1: Ingest Scoping Questions
Receive the list of scoping questions and hypotheses approved during the discovery phase.
- Break down the list of questions into discrete EDA tasks.

### Step 2: Parallel Basic EDA Execution
Spawn **multiple specialized subagents in parallel** to perform basic Exploratory Data Analysis (EDA) on each discrete task.
- Create initial notebooks in `outputs/run_YYYYMMDD_HHMMSS/01_baseline_X.ipynb` for each question (e.g., `01_baseline_retention.ipynb`, `01_baseline_monetization.ipynb`).
- Run these notebooks programmatically in parallel to calculate broad rates, totals, averages, and distributions.

### Step 3: Local Storage & Preparation for Review
Store all relevant outputs securely.
- Explicitly store the generated data, tables, charts, and statistics locally in the active run directory.
- Compile a detailed audit trail of all baseline notebooks created and ran.
- Format these results so they are ready for the Expert Reviewer agent to consume.

## Output Contract
Return a Markdown report containing:
- **Execution Audit Table** displaying the parallel run tree of baseline notebooks and their target scopes.
- Confirmation that all output data and statistics are stored locally for the reviewer.
