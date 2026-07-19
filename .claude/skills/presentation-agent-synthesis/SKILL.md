---
name: presentation-agent-synthesis
description: Translates notebook data points into McKinsey/BCG style slide-by-slide outlines using the Pyramid Principle.
risk: safe
date_added: "2026-07-19"
version: "1.0.0"
---

# Presentation Agent: McKinsey/BCG Consulting Synthesis

This skill translates statistical results into a structured management presentation narrative. It applies consulting frameworks to focus only on highly critical insights that lead to strategic recommendations.

## When to Use

Use this skill after the analysis notebooks are successfully run and you need to structure the slide outlines before rendering them as code.

## Core Consulting Guidelines

### 1. The Minto Pyramid Principle
- **Top Down**: Start with the overarching strategic recommendation (e.g., "Implement senior-focused authentication to save $240k monthly").
- **Supporting Pillars**: Break this recommendation into 3-4 structured slide themes (e.g., Channel Performance, Drop-off Analysis, Remediation Cost).
- **Data Proof**: Base every supporting point on exact metrics generated in the notebooks.

### 2. Active Message Headlines
- Never write passive titles (e.g., "Revenue Trends" or "Failed Logins").
- Every slide title must be an active, complete statement explaining the *what* and *why* (e.g., "Web Login Failures are Flat, While Mobile Success Rates Dropped 14% Since December").

### 3. McKinsey/BCG Structured Slide Layouts
- **Header**: Single declarative sentence bold active headline.
- **Core Grid (2-Column Slide Layout)**:
  - **Left Column (Visual)**: Custom Economist-style vector chart or table containing key value markers and highlight annotations.
  - **Right Column (Context/Text)**: A **Key Takeaways Panel** containing 2-3 bullet points with bold lead-in summaries (e.g., **• Segment Outlier**: Cashback cards represent a disproportionate 4.8% churn...).
- **Footer**: Attribution footnote (e.g. *"Source: E-Commerce Transaction Logs, 2024-2025"*) and Slide count.

## Ordered Steps

### Step 1: Ingest Notebook Outputs
- Scan the generated notebook trail to pull out key statistics, coefficients, outlier peaks, and totals.

### Step 2: Establish Presentation Narrative Outline
- Structure the deck to fit standard McKinsey/BCG flow (Executive Summary, Market/Revenue Trends, Friction Points/Leakage, Opportunities, Remediation Impact).

### Step 3: Outline Each Slide
Draft each slide to enforce the 2-column layout:
1. **Slide Title**: Bold active statement.
2. **Slide Subtitle**: Brief context.
3. **Left Column (Visual Specification)**: Chart type, specific labels, and target SVG annotations.
4. **Right Column (Bullet points)**: Structured Key Takeaways list with bold leading words.
5. **Footer**: Data source attribution.

## Output Contract
Return a Markdown presentation storyboard specifying:
- Title, subtitle, slide sequence, 2-column data mapping, and the consulting rationale behind each slide's structure.

