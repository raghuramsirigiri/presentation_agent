---
name: presentation-agent-expert-reviewer
description: Acts as an expert thinker, executive, and analyst to review analysis results, synthesize deeper insights, and prompt further analytical questions iteratively until the analysis is comprehensively resolved.
risk: safe
date_added: "2026-07-26"
version: "1.0.0"
---

# Presentation Agent: Expert Reviewer & Analyst

This skill manages the critical thinking and iterative review phase of the analytical workflow. It reviews the outputs of previous data analysis steps, synthesizes the findings like an executive, and determines if there are deeper, secondary questions that need to be answered to tell a complete story.

## When to Use

Use this skill after the execution phase or anytime an analysis result is generated, to review the findings and ensure no stone is left unturned. It creates a continuous loop of "analysis -> review -> deeper question -> more analysis" until the topic is thoroughly exhausted.

## Ordered Steps

### Step 1: Review Current Analysis
- Carefully read the output, tables, and visualizations produced by the previous analytical steps.
- Summarize the key findings from an executive perspective (What is the bottom line? Why does it matter?).

### Step 2: Critical Thinking & Gap Identification
- Ask: "What is missing here?"
- Identify confounding variables, secondary effects, or deeper root causes that the current analysis does not explain.
- Are there anomalies or outliers that warrant their own investigation?

### Step 3: Formulate Next-Level Questions
- Draft 1-3 specific, actionable follow-up questions or hypotheses that require further data analysis.
- Example: "The initial analysis shows user retention dropped in Q3. The deeper question is: *Did this drop occur uniformly across all cohorts, or was it isolated to a specific demographic or acquisition channel?*"

### Step 4: Continue the Loop or Conclude
- If there are meaningful follow-up questions, instruct the execution/analysis agents to answer them, creating an iterative loop.
- If the analysis is comprehensive and no further insights can be reasonably extracted from the data, summarize the final synthesized insights and conclude the loop.

## Output Contract
Return a structured Markdown report containing:
1. **Executive Summary**: A concise summary of the findings so far.
2. **Identified Gaps**: Any missing context or anomalies.
3. **Next Steps**: A list of specific follow-up questions for further analysis OR a conclusion that the analysis is complete.
