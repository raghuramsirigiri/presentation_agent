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

### Step 1: Baseline Analysis & Execution
Divide the approved business scope into baseline modules.
- Create initial notebooks in `outputs/run_YYYYMMDD_HHMMSS/01_baseline_X.ipynb` to calculate broad rates, totals, averages, and distributions.
- Run these notebooks programmatically using Python execution redirection to capture basic tables and statistics.

### Step 2: Cognitive Evaluation & Deep-Dive Triggering
Examine the baseline or previous loop's results. You must act as a lead analyst: deeply understand the findings and actively search for deeper, more meaningful analysis that can be performed. Look at ALL the results collectively and *think* critically.
Your primary goal is to form new hypotheses and push the analysis further. Ask yourself: "What new questions do these results raise? What deeper data slices or cross-correlations could explain these trends?" 
Based on this cognitive reflection, outline the new follow-up deep-dive questions you will investigate.



### Step 3: Deep-Dive Analysis Execution (Subagent Loop)
Spawn specialized subagents to build and run deep-dive notebooks in the run folder:
- **Format**: `outputs/run_YYYYMMDD_HHMMSS/0X_deepdive_topic.ipynb` (e.g., `05_deepdive_cac_decay.ipynb`).
- Perform cohort decay modeling, correlation regressions, and contribution analysis based on the hypotheses you generated in Step 2.

### Step 4: Iterative Loop Termination
Review the deep-dive outputs collectively. Loop back to Step 2 and *think* again to find even deeper, meaningful analysis based on the latest results. You must continue to deep dive until you can't find any more answers or run out of data.
Terminate the loop ONLY when all of the following conditions are met:
1. **Minimum Iterations**: You have executed **more than 1 loop**. You MUST NEVER stop after just the initial baseline analysis.
2. **Exhaustion of Data/Insights**: You have pushed for deeper analysis and are confident that absolutely no further meaningful, strategic answers can be found, or no further data exists to support deeper cuts.
3. **Maximum Depth**: The iterative loop hits the hard limit of **5 levels of depth**.

### Step 5: Map the Trail Log
Compile a detailed audit trail of all baseline and deep-dive notebooks, highlighting the lineage (e.g., how baseline results in notebook `01` triggered deep-dive calculations in notebook `05`).

## Output Contract
Return a Markdown report containing:
- **Lineage Audit Table** displaying the hierarchical run tree:
  - Baseline Notebook (Path, Key Metrics, Trigger Rule)
  - Deep-Dive Notebook (Path, Target Anomaly, Deeper Insights)
- Status checks ensuring all notebooks ran top-to-bottom with persistent states.


