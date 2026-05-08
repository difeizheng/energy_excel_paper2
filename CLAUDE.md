# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Chinese academic paper project targeting **《计算机工程与应用》** (Chinese core journal). The paper studies knowledge graph construction for Excel financial models in the energy sector, using a real pumped-storage hydropower station financial evaluation model as the case study.

## Repository Structure

| Path | Content |
|------|---------|
| `CHINESE-JOURNAL-OF-COMPUTERS--Overleaf-Latex-Template/` | Clean LaTeX template (CjC class + .sty files). Paper content to be generated from scratch. |
| `数字化系统财务模型边界【抽水蓄能】v12.xlsx` | Source Excel financial model (14 sheets, 42,109 formulas) |
| `experiment_report.txt` | All empirical statistics — **single source of truth for numbers** |
| `ablation_results.json` | Ablation experiment results (n=299) |
| `energy_kg_paper_skill_v2.md` | **Primary writing guide** (latest version, aligned with real experiment data) |
| `energy_kg_paper_skill.md` | Legacy v1 writing guide (reference only, some numbers outdated) |
| `energy_kg_system.zip` | System source code (5 modules) |
| `fig1_data_flow.png`, `fig2_formula_dist.png`, `fig3_dependency_heatmap.png` | Paper figures |
| `paper_draft.docx` | Current paper draft (Word format, reference only) |

## LaTeX Entry Point

Create `main.tex` in `CHINESE-JOURNAL-OF-COMPUTERS--Overleaf-Latex-Template/` based on `CjC_template_tex.tex` as starter template. Paper sections will be split into separate `.tex` files and included via `\input`.

**Paper structure (7 sections, per Skill B-1):**
1. 引言 (background, related work, contributions)
2. 抽水蓄能财务模型特征分析
3. Excel解析与语义理解方法
4. 知识图谱构建
5. 智能问答系统
6. 实验与评估 (most important section)
7. 结论

**LaTeX compilation:** Use **XeLaTeX** compiler (required by the template). Other compilers may fail to produce PDF.

**Data verification:** All statistics come from `experiment_report.txt` and `ablation_results.json`. Never invent or modify numbers.

## Core Claims (DO NOT MODIFY)

Three core numbers that must be consistent everywhere in the paper:
1. Ablation: method A = 20.7% accuracy vs methods B/C = 88.3% (n=299)
2. IRR path tracing: <0.5s response time (vs 45-60min manual, >5,000x improvement)
3. QA intent recognition: 92.3% accuracy (n=13)

Additional invariant statistics from `experiment_report.txt`:
- 42,109 formulas, 9,199 cross-sheet references, 14 sheets
- DAG: 62,160 nodes, 78,472 edges, longest path 730 steps
- 289 error formulas (0.69%)
- KG: 42,138 entities, 65,333 relations

## Writing Rules (MANDATORY)

When writing or editing any paper content (`.tex` files, abstract, conclusion, etc.), **follow all guidelines in `energy_kg_paper_skill_v2.md`**:
- All ablation numbers must match `ablation_results.json`: Method A = 20.7%/7.9%/37.1%, Method B/C = 88.3%/81.7%/99.0%
- Enforce banned-word check (0 matches for 赋能/闭环/显著提升/深度融合 etc.)
- Maintain number consistency across all sections (see Core Claims above)
- Follow the 7-section structure defined in v2
- Apply the conclusion 4-paragraph template from v2 Section 7
- Apply digital consistency checklist from v2 after any edits

**Key highlights:**
- **"资本金/全投资双视角" and "跨业务Sheet现象"** must each have independent paragraphs in Section 2
- **Ablation section (6.2)** must include three findings with the 28/35 error detail
- **Conclusion** must be 4 prose paragraphs, not numbered lists
- **Abstract ending** must use the efficiency improvement number, not generic "提供支撑" phrases

## System Code

`energy_kg_system.zip` contains the analysis system (5 modules). Unzip to examine implementation details referenced in the methods section. The system parses the Excel model, builds the dependency DAG, performs semantic understanding, constructs the knowledge graph, and provides QA capabilities.
