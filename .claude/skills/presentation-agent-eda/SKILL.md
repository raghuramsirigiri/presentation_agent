---
name: presentation-agent-eda
description: Specializes in Exploratory Data Analysis (EDA) in the loop, identifying distributions, outliers, and patterns before deep dive execution.
risk: safe
date_added: "2026-07-28"
version: "1.0.0"
---

# Presentation Agent: Exploratory Data Analysis (EDA)

This skill manages the specialized Exploratory Data Analysis phase, acting as an in-the-loop analyst that examines the shape, distributions, and anomalies of the data before deep-dive models or synthesis are executed.

## When to Use

Use this skill after the initial discovery phase (when schemas are parsed and hypotheses are formulated) but before complex execution or deep-dive subagents are spawned. It ensures the data is thoroughly understood and validated.

## Ordered Steps

### Step 1: Univariate Analysis
Run comprehensive univariate checks on all key features relevant to the agreed-upon hypotheses.
- Analyze numeric distributions (mean, median, standard deviation, skewness, kurtosis).
- Identify and quantify missing values and formulate imputation or handling strategies.
- Detect outliers using interquartile range (IQR) or Z-scores.
- Analyze categorical variables for cardinality and frequency distributions.

### Step 2: Bivariate & Multivariate Analysis
Examine relationships between variables to surface initial insights.
- Calculate correlation matrices for numeric features.
- Generate cross-tabulations for categorical features.
- Identify preliminary trends or patterns (e.g., scatter plot relationships, box plots across categories).
- Look for collinearity among features that might affect downstream modeling.

### Step 3: Anomaly & Data Quality Deep-Dive
Actively search for data quality issues that could derail the analysis.
- Check for temporal inconsistencies (e.g., sudden drops in volume over time).
- Flag illogical values (e.g., negative ages, dates in the future).
- Document all required data cleaning steps for the execution phase.

### Step 4: Iterative Insight Refinement (In the Loop)
Review the EDA findings critically.
- Refine the initial business hypotheses based on what the data actually shows.
- If the data contradicts a hypothesis, document this early finding.
- Recommend specific deep-dive execution strategies based on the identified patterns and data characteristics.

## Output Contract
Return a Markdown EDA report containing:
- **Data Quality Summary**: Key issues identified (missingness, outliers, anomalies) and recommended fixes.
- **Key EDA Insights**: 3-5 preliminary findings from univariate and bivariate analysis that inform the hypotheses.
- **Execution Recommendations**: Specific guidance for the `presentation-agent-execution` phase based on the EDA.
