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
Examine the baseline results. Instead of just programmatically looking for statistical anomalies, you must act as a lead analyst. Look at ALL the results collectively and *think* about what further analysis can be done based on the existing findings.
While you should still calculate dynamic limits (like IQR outliers, Pareto cuts, and funnel leakage), your primary goal is to form new hypotheses. Ask yourself: "What new questions do these results raise? What data slices or cross-correlations could explain these trends?" 
Based on this cognitive reflection, outline the new follow-up questions you wish to investigate.



### Step 3: Deep-Dive Analysis Execution (Subagent Loop)
Spawn specialized subagents to build and run deep-dive notebooks in the run folder:
- **Format**: `outputs/run_YYYYMMDD_HHMMSS/0X_deepdive_topic.ipynb` (e.g., `05_deepdive_cac_decay.ipynb`).
- Perform cohort decay modeling, correlation regressions, and contribution analysis based on the hypotheses you generated in Step 2.

### Step 4: Iterative Loop Termination
Review the deep-dive outputs collectively. Loop back to Step 2 and *think* again if any further analysis can be done based on these new results. 
Terminate the loop only when:
1. You have evaluated all results and are satisfied as an analyst that no further meaningful, strategic hypotheses can be explored with the available data.
2. The loop maxes out at **5 levels of depth**.

### Step 5: Map the Trail Log
Compile a detailed audit trail of all baseline and deep-dive notebooks, highlighting the lineage (e.g., how baseline results in notebook `01` triggered deep-dive calculations in notebook `05`).

## Output Contract
Return a Markdown report containing:
- **Lineage Audit Table** displaying the hierarchical run tree:
  - Baseline Notebook (Path, Key Metrics, Trigger Rule)
  - Deep-Dive Notebook (Path, Target Anomaly, Deeper Insights)
- Status checks ensuring all notebooks ran top-to-bottom with persistent states.


