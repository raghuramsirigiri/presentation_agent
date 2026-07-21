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

### Step 2: Programmatic Anomaly & Deep-Dive Triggering
Examine the baseline results programmatically for statistical anomalies and pivot opportunities. **Do not use hardcoded thresholds.** Instead, calculate limits dynamically based on the dataset's active distribution:
- **Spikes & Outliers**: Detect dynamically using Interquartile Range (IQR) outliers (values exceeding $Q3 + 1.5 \times IQR$) or standard Z-scores ($|Z| > 2.0$ computed relative to the active column's distribution).
- **Funnel Leakage**: Identify drop-off phases showing a statistically significant decrease compared to the average funnel stage delta.
- **Risk & Churn Concentrations**: Filter segments falling into the upper quartile ($Q3$, top 25%) of churn or refund rate distributions.
- **Segment Pivots**: Use Pareto calculations (80/20 cuts) to isolate the minimum subset of categories, demographics, or regions that account for at least 80% of total activity or revenue.
- **Zero-Variance Fallbacks**: If standard deviations or distributions show zero variance, fall back dynamically to percentile cuts, raw sorting distributions, or default range bounds to prevent mathematical errors (such as division by zero) and ensure the subagent loops never stall.
Based on these dynamically identified outlier segments, trigger subsequent deep-dive subagent notebooks to analyze root causes.



### Step 3: Deep-Dive Analysis Execution (Subagent Loop)
Spawn specialized subagents to build and run deep-dive notebooks in the run folder:
- **Format**: `outputs/run_YYYYMMDD_HHMMSS/0X_deepdive_topic.ipynb` (e.g., `05_deepdive_cac_decay.ipynb`).
- Perform cohort decay modeling, correlation regressions, and contribution analysis on the isolated anomaly subsets.

### Step 4: Iterative Loop Termination
Review the deep-dive outputs. If new secondary outliers or correlations are found, spawn another iteration layer (up to 3 levels of depth). Terminate the loop only when:
1. All variances in the core metrics have been broken down to their lowest-level granular pivots.
2. The statistical confidence of secondary correlations drops below 90% (p-value > 0.1).
3. No further data slices can be extracted from the target datasets.

### Step 5: Map the Trail Log
Compile a detailed audit trail of all baseline and deep-dive notebooks, highlighting the lineage (e.g., how baseline results in notebook `01` triggered deep-dive calculations in notebook `05`).

## Output Contract
Return a Markdown report containing:
- **Lineage Audit Table** displaying the hierarchical run tree:
  - Baseline Notebook (Path, Key Metrics, Trigger Rule)
  - Deep-Dive Notebook (Path, Target Anomaly, Deeper Insights)
- Status checks ensuring all notebooks ran top-to-bottom with persistent states.


