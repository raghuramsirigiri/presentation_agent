# Notebook Presentation Creator (CLI Skill)

This skill automates the end-to-end translation of local datasets and codebases into C-suite-ready slides. It scans the current directory for variables, tables, and scripts; proposes data hypotheses to the user; implements the analysis using a modular notebook trail; and compiles the results into a McKinsey-style PDF or HTML presentation with Economist-style CSS/SVG charts.

## Installation

### Automatic Setup
Simply symlink this skill to your platform-specific skills folder:

```bash
# For Claude Code
mkdir -p ~/.claude/skills
ln -sf "$(pwd)/.claude/skills/notebook-presentation-creator" ~/.claude/skills/notebook-presentation-creator
```

## Features

1. **Workspace Discovery**: Automatically discovers files including `.csv`, `.xlsx`, `.ipynb`, `.py`, `.ppt`, and `.pptx` in the project.
2. **Analytical Scoping**: Suggests data expansion plans and requests direct inputs on what business questions to answer.
3. **Execution Trail**: Spawns subagents to carry out data cleaning, modeling, or statistics, saving separate notebooks for verification.
4. **Expert Consulting Synthesis**: Drafts structured consulting outlines using the Minto Pyramid Principle and message-driven active slide headers.
5. **Economist Chart Aesthetics**: Custom-renders CSS/SVG charts matching *The Economist*’s editorial visual theme.
6. **Viewport-Optimized Slides**: Uses viewport-relative CSS rules (`clamp()`, `height: 100vh`) to prevent vertical scrolling.

## How to Trigger the Skill

Invoke the skill in your agent session using triggers such as:
- `create consulting deck from notebook`
- `analyze notebook and present insights`
- `generate McKinsey style presentation from python data`

---

## Directory Structure

```
notebook-presentation-creator/
├── SKILL.md                 # Core instructions and workflow definition
├── README.md                # This documentation
├── references/              # Style templates, layout helpers
└── examples/                # Example slides and chart structures
```
