# ARC Prize 2025: Abstract Reasoning Challenge 🧩

[![Korean](https://img.shields.io/badge/Language-Korean-blue)](#) [🇰🇷 한국어로 읽기](./README_ko.md)

![Kaggle](https://img.shields.io/badge/Kaggle-Competition-blue?logo=kaggle)
![Status](https://img.shields.io/badge/Status-Completed-success)

This repository contains my approach and evolution of solutions for the [ARC Prize 2025 Kaggle Competition](https://www.kaggle.com/competitions/arc-prize-2025). The Abstraction and Reasoning Corpus (ARC) is a benchmark designed to measure the general intelligence (AGI) of AI systems by evaluating their ability to solve novel, few-shot reasoning tasks.

## 📁 Project Structure

The project has been dynamically refactored and organized for better maintainability:

- `notebooks/` - Contains the Kaggle submission scripts and notebook iterations (`kaggle_notebook_v1` to `v10`).
- `solvers/` - Core solver modules implementing different strategies (e.g., `hybrid_solver.py`, `perfect_solver.py`, `ensemble_solver.py`).
- `dsl/` - Domain Specific Language implementations for program synthesis (`arc_dsl_v1.py`, etc.).
- `analysis/` - Scripts for exploratory data analysis (EDA), pattern detection, and task investigation.
- `evaluators/` - Local evaluation scripts to test solvers against validation datasets.
- `results/` - Local evaluation results and JSON outputs.
- `utils/` - Helper scripts for downloading data, format validation, and Kaggle submissions.
- `docs/` - Progress reports and competition summaries.

## 🧠 Methodology & Evolution

The solver strategy evolved through multiple iterations (up to Version 10), progressively combining rule-based heuristics with programmatic synthesis and pattern extraction.

### Early Iterations (V1 - V5)
- **Direct Matching:** Implemented basic geometric transformations (rotation, flipping, transposition).
- **Scaling & Cropping:** Added logic for 2x/3x scaling and extracting non-zero areas.
- **Color Operations:** Introduced basic color inversion, shifting, and modular arithmetic.

### Advanced Hybrid Approaches (V8 - V10)
Version 10 (`EnhancedHybridSolver`) represents the culmination of this effort, featuring a 3-step prioritized pipeline:
1. **DSL Program Search (High Priority):** Rapidly searches single and common two-operation combinations from a predefined set of primitives (Identity, Geometric, Scaling, Cropping, Color).
2. **Transform Search:** Checks a broader set of 50+ custom-defined transformations verified against the training examples.
3. **Learning-based Extraction (Fallback):** Attempts to derive size ratios, consistent color mappings (>80% agreement), and repeating patterns (Detect and Extend) if no exact program is found.

## 📊 Results

- **Kaggle Public Leaderboard Score:** `1.67`
  - **Rank:** Top 45% (~651st out of 1,456 teams)
  - **Difference from 1st place:** 25.97 points behind the winning score of 27.64 (NVARC team)
- **Local Evaluation (V10):** `0.0` Exact Accuracy, though yielding high partial-correctness scores (up to ~98.9% pixel matching) on complex tasks.

## 🔍 Critical Analysis

Despite significant engineering effort in building an extensive DSL and hybrid search mechanism, the results highlight the fundamental difficulty of the ARC benchmark:

1. **The Limit of Hand-Crafted DSLs:** The current implementation heavily relies on predefined geometric and color operations. While this solves tasks that strictly adhere to these specific transformations, it entirely fails on tasks requiring novel abstractions, counting, object tracking, or physics-like interactions. The search space for combining primitives grows exponentially, making deep program synthesis computationally unfeasible within the 12-hour Kaggle limit.
2. **"Pixel-Perfect" Penalty:** The pass@2 evaluation metric is unforgiving. A solution with 98.9% pixel accuracy still scores a 0 for the task. The solver often identified the correct general transformation (e.g., scaling or moving an object) but failed on edge cases or background noise.
3. **Lack of True Generalization:** Rule-based pattern matching (e.g., learning size ratios or 1:1 color mappings) does not equate to "reasoning". True generalization requires the system to understand "objects", "containment", and "intent", which matrix manipulations cannot easily capture.

## 🚀 Next Steps & Future Directions

To achieve a competitive score (closer to the current top tier of ~27% or the Grand Prize threshold of 85%), the approach must pivot from strict programmatic search to neuro-symbolic or foundation model approaches:
- **Test-Time Training (TTT) / Fine-tuning:** Training lightweight Vision Transformers (ViT) or 1D sequence models on the test examples specifically.
- **LLM-assisted Program Synthesis:** Generating Python or DSL code dynamically using open-weights models (if computationally viable).
- **Object-Centric Representations:** Moving away from raw numpy grids to graph-based or object-oriented representations of the input spaces prior to transformation.

<!-- BLOG-URL:START -->

## Blog

- Blog note: [ARC Prize 2025: Abstract Reasoning Challenge 🧩](https://softkleenex.github.io/coding_training/kaggle/kaggle-arc-prize-2025)

<!-- BLOG-URL:END -->
