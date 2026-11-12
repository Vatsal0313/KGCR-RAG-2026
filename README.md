# Welcome to the KG Construction, Reasoning, and RAG Project Group (KGR-RAG PG)

## Next meeting:
- Thursday, 12 November 2026, PG Meeting, in room FU.519 from 14:30 to 16:30.
  Agenda:
  - Short technical presentation related to reproducing the model.
  - Discuss the results and findings

## Materials
- Presentation templates:
  - [PPT](https://github.com/dice-group/KGCR-RAG-2026/blob/main/DICE%20Power%20Point%20Design%20NEW.pptx)
  - [Latex](https://github.com/dice-group/KGCR-RAG-2026/blob/main/DICE_presentation_template_in_latex.zip) 
- Report template:
  LNCS [https://www.overleaf.com/latex/templates/springer-lecture-notes-in-computer-science/kzwwpvhwnvfj](https://www.overleaf.com/latex/templates/springer-lecture-notes-in-computer-science/kzwwpvhwnvfj)
     
## KGCR-RAG PG Two-Weekly Tasks Summary

Visit this [link](https://github.com/dice-group/KGCR-RAG-2026/blob/main/regular-tasks.md) for the regular task for the details

## Short Technical Report Template
### [Formal Title: e.g., Reproducing [Model Name]]

**Author:** [Full Name] ([Matriculation Number])  
**Affiliation:** [Project Group / Department, University]  
**Date:** [Month Year]

### Abstract
[150–200 words summarizing: (1) the target paper/system being reproduced, (2) the experimental constraints or modifications applied, (3) the main quantitative results compared to the reported baseline, and (4) the primary root causes identified in error analysis.]

---

### 1. Introduction and System Overview
[Paragraph 1: Context and objective. Introduce the original work [1], its core claim, and the goal of this reproduction study.]

[Paragraph 2: System architecture. Describe the pipeline stages objectively in prose, referencing a figure or compact table.]

| Stage | Component / Module | Function |
| :--- | :--- | :--- |
| 1 | [Module A] | [Concise description of input, processing, and output] |
| 2 | [Module B] | [Concise description of input, processing, and output] |
| 3 | [Module C] | [Concise description of input, processing, and output] |

---

### 2. Experimental Setup
* **Dataset & Metrics:** [Name the benchmark dataset(s) [2], subset size evaluated, and exact evaluation metrics (e.g., Accuracy, Hits@1).]
* **Models & Hyperparameters:** [Specify backbone LLMs, embedding models, context lengths, temperature settings, and any caps/thresholds.]
* **Environment & Implementation Notes:** [State hardware/OS specs and summarize any required bug fixes or environment patches in 1–2 sentences.]

---

### 3. Results and Error Analysis
[Paragraph 1: High-level summary of quantitative performance compared to the original paper.]

| Benchmark / Subset | Reported Baseline | Reproduced Result | Delta ($\Delta$) |
| :--- | :---: | :---: | :---: |
| [Dataset / Split 1] | 93.33% | 68.00% | -25.33 pp |
| [Dataset / Split 2] | 74.70% | 87.50% | +12.80 pp |

#### Error Analysis
[Group observed failures into 2–4 distinct analytical categories with concrete examples:]

---

### 4. Limitations and Conclusion
[Paragraph 1: Threats to validity and architectural limitations (e.g., smaller parameter count, sample size, privacy leaks, or fallback behavior).]

[Paragraph 2: Final synthesis of what was successfully verified, key lessons learned, and 2–3 concrete directions for future work.]

---

### References
Please follow the template provided

## Communication platform and tools
Communication platforms and tools that can be used in this PG:

1. Elements messaging
   Real-time chat for day-to-day coordination and quick questions. We can ask for an invitation to join the group chat.
   
   → [Join the Elements group](https://element.cs.uni-paderborn.de/)

3. Sciebo cloud storage
   Shared, versioned space for project files and documents. Use it to upload, review, and collaborate on materials.

   → [Open the Sciebo folder](https://uni-paderborn.sciebo.de/)

4. Weekly report form
  Submit your report at the start of each week. Share progress, blockers, and planned next steps so we can prepare for the meeting.

   Please complete the form before the weekly meeting.

   → [Fill out the weekly report form](https://umfragen.uni-paderborn.de/index.php/563876?lang=en)
